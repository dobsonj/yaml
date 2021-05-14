
# Creating a persistent volume using dynamic provisioning

## Create a PersistentVolumeClaim

```
$ kubectl apply -f pvc_claim1_thin-csi_1gb.yaml
persistentvolumeclaim/claim1 created
```

## Bind it to a new Pod

```
$ kubectl apply -f pod_ubuntu_claim1_sleep.yaml
pod/ubuntu created
```

## Check if the PVC, PV, and Pod were provisioned successfully

```
$ kubectl get pvc
NAME     STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
claim1   Bound    pvc-26a9e788-cd92-4de2-b4bd-25001e6f49b3   1Gi        RWO            thin-csi       35s

$ kubectl get pv
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM            STORAGECLASS   REASON   AGE
pvc-26a9e788-cd92-4de2-b4bd-25001e6f49b3   1Gi        RWO            Delete           Bound    default/claim1   thin-csi                29s

$ kubectl get pods
NAME     READY   STATUS    RESTARTS   AGE
ubuntu   1/1     Running   0          42s
```

## Get a shell in the running pod

```
$ kubectl exec -it ubuntu -- /bin/bash
root@ubuntu:/# df -h | grep claim1
/dev/sdb        976M  2.6M  907M   1% /mnt/claim1
```

