# Simple NFS server / client test in k8s

## Sources

[Sharing Persistent Disks on Multiple Nodes in Kubernetes Using NFS](https://medium.com/swlh/quick-fix-sharing-persistent-disks-on-multiple-nodes-in-kubernetes-ef5541fd8376)

## Setup NFS server deployment in k8s cluster

```
$ kubectl apply -f pvc_for_nfs.yaml
persistentvolumeclaim/pvc-for-nfs created
$ kubectl apply -f nfs_server.yaml
deployment.apps/nfs-server created
service/nfs-server created
$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
nfs-server-7597576485-fhbqf   1/1     Running   0          44s
```

## Create a NFS PV and NFS client pod

```
$ kubectl apply -f nfs_volume.yaml
persistentvolume/nfs created
persistentvolumeclaim/nfs created
$ kubectl apply -f nfs_client.yaml
deployment.apps/nfs-busybox created
```

