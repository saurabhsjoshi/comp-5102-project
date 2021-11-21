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
1. Start 3 node K8s cluster `minikube start --nodes 3 -p rook-project`
2. Check storage devices have no parition by doing `lsblk -f`
3. Add helm repo for rook `helm repo add rook-release https://charts.rook.io/release`
4. Deploy Rook operator 
```commandline
helm repo add rook-release https://charts.rook.io/release
helm install --create-namespace --namespace rook-ceph rook-ceph rook-release/rook-ceph
```
5. Make sure Rook operator is running `kubectl -n rook-ceph get pod`
6. Create the Ceph cluster 