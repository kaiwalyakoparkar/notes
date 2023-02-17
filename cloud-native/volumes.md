# Volumes 

![Flow diagram](https://i.imgur.com/KaizGfd.png)

## volumes.yml

```yml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nginx-pv
spec:
  capacity:
    storage: 500Mi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: local-storage-example #className we specified in pvc
  local:
    path: /usr/share/nginx/html
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: kubernetes.io/hostname
              operator: In
              values:
              - nodel
```

## volume-claim.yml

```yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nginx-pvc #Name that we referred into deployment file
spec:
  volumeName: nginx-pv
  storageClassName: local-storage-example #A claim can request a particular class by specifying the name of a StorageClass using the attribute storageClassName. Only PVs of the requested class, ones with the same storageClassName as the PVC, can be bound to the PVC.
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```