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
DISK="/dev/sdg" && \
sudo sgdisk --zap-all $DISK && \
sudo dd if=/dev/zero of="$DISK" bs=1M count=100 oflag=direct,dsync && \
sudo blkdiscard $DISK
```
2. Start 3 node K8s cluster `minikube start --nodes 3 -p rook-project --cpus 6 --memory 8g`
3. Check storage devices have no parition by doing `lsblk -f`
4. Add helm repo for rook `helm repo add rook-release https://charts.rook.io/release`
5. Deploy Rook operator 
```commandline
helm install --debug --create-namespace --namespace rook-ceph rook-ceph rook-release/rook-ceph
```
6. Make sure Rook operator is running `kubectl -n rook-ceph get pod`
7. Create the Ceph cluster. WARNING: Make sure you check all the attributes in values-override.yaml (device filters etc)
```commandline
helm install --debug --create-namespace --namespace rook-ceph rook-ceph-cluster \
   --set operatorNamespace=rook-ceph rook-release/rook-ceph-cluster -f values-override.yaml
```
8. Check Ceph cluster status `kubectl -n rook-ceph get cephcluster`
8.1. To delete Ceph cluster 
```commandline
helm delete --namespace rook-ceph rook-ceph-cluster
minikube delete --all
```

## Accessing K8s dashboard
If using minikube just run `minikube -p rook-project dashboard` to get dashboard. Otherwise manually deploy:
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

## Deploy application with PVC
1. Use the YAML to deploy app: `kubectl apply -f app.yaml`
2. To remove deployment: `kubectl delete -f app.yaml`

## Access dashboard
1. Start K8s proxy: `kubectl -n rook-ceph proxy`
2. Go to URL: http://localhost:8001/api/v1/namespaces/rook-ceph/services/https:rook-ceph-mgr-dashboard:https-dashboard/proxy/
3. Get password : `kubectl -n rook-ceph get secret rook-ceph-dashboard-password -o jsonpath="{['data']['password']}" | base64 --decode | xclip -sel clip`


## Mounting Drive inside Minikube VM
1. Create directory for mount point: `sudo mkdir -p /mnt/drive`
2. Mount drive: `sudo mount /dev/sdc1 /mnt/drive`