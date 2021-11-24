# Steps followed:

## Installation
Install the following:
1. docker
2. kubectl
3. minikube
4. lvm (optional for ceph)
5. Linux module called RBD (Can check if exists by doing `modprobe rbd`)
6. helm

## Commands to run
1. Disks need to be cleaned everytime a new cluster is created
```commandline
# For each disk
DISK="/dev/sde" && \
sudo sgdisk --zap-all $DISK && \
sudo dd if=/dev/zero of="$DISK" bs=1M count=100 oflag=direct,dsync && \
sudo blkdiscard $DISK
```
2. Start 4 node K8s cluster `minikube start --nodes 4 -p rook-project`
3. Check storage devices have no parition by doing `lsblk -f`
4. Add helm repo for rook `helm repo add rook-release https://charts.rook.io/release`
5. Deploy Rook operator 
```commandline
helm install --create-namespace --namespace rook-ceph rook-ceph rook-release/rook-ceph
```
6. Make sure Rook operator is running `kubectl -n rook-ceph get pod`
7. Create the Ceph cluster. WARNING: Make sure you check all the attributes in values-override.yaml (device filters etc)
```commandline
helm install --create-namespace --namespace rook-ceph rook-ceph-cluster \
   --set operatorNamespace=rook-ceph rook-release/rook-ceph-cluster -f values-override.yaml
```
8. Check Ceph cluster status `kubectl -n rook-ceph get cephcluster`
8.1. To delete Ceph cluster 
```commandline
helm delete --namespace rook-ceph rook-ceph-cluster
minikube delete --all
```

## Setting up Rook toolbox
1. Create `kubectl create -f cluster/examples/kubernetes/ceph/toolbox.yaml`
2. Rollout `kubectl -n rook-ceph rollout status deploy/rook-ceph-tools`
3. Exec `kubectl -n rook-ceph exec -it deploy/rook-ceph-tools -- bash`
4. Run `ceph status` to get status of the cluster or `ceph -w`for watching status

## Accessing K8s dashboard
1. Install dashboard on cluster
```commandline
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.4.0/aio/deploy/recommended.yaml
```
2. Create required user accounts
```commandline
kubectl apply -f service-account.yaml && \
kubectl apply -f user-binding.yaml
```
3. Start proxy `kubectl proxy`
4. Copy token to clipboard
```commandline
kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"  | xclip -sel clip
```
5. Go to dashboard http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/ and paste token
