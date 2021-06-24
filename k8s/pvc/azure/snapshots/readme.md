
# CSI snapshot example on Azure

## Create volumesnapshotclass

```
$ kubectl apply -f volumesnapshotclass.yaml
volumesnapshotclass.snapshot.storage.k8s.io/csi-snapshotclass created
```

## Create PVC and pod

```
$ kubectl apply -f pvc_claim1_managed-csi_1gb.yaml
persistentvolumeclaim/claim1 created
$ kubectl apply -f pod_ubuntu_claim1_sleep.yaml
pod/ubuntu created
$ kubectl get pods
NAME     READY   STATUS    RESTARTS   AGE
ubuntu   1/1     Running   0          34s
```

## Create volume snapshot

```
$ kubectl apply -f volumesnapshot.yaml
volumesnapshot.snapshot.storage.k8s.io/claim1-snapshot1 created
```

