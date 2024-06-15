# Docker Storage

- When it comes to storage in docker it depends on two things
  1. Storage Drivers
  2. Volume Drivers

## Storage Drivers

`/var/lib/docker/`
  - `aufs/`
  - `containers/`
  - `image/`
  - `volumes/`

## Volumens (On K8s)

```yaml
spec:
  containers:
  - image: nginx
    name: nginx
    volumeMounts:
    - mountPath: /opt
      name: data-volume
  volumes:
  - name: data-volume
    hostPath:
      path: /data
      type: Directory
```

```yaml
path: /data
type: Directory
```
This is alright for single node but we want data for all/ multiple nodes hence we don't use this.

## Persistent Volumes

```yaml
kind: PersistentVolume
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 1Gi
  hostPath:
    path: /data
    type: Directory
```

## Persistent Volume Claim

- 
  ```yaml
  kubectl get pvc
  ```
- 
  ```yaml
  kubectl delete pvc <name>
  ```
- We can decide what happens to pv after pvc is deleted. This can be done using 
  - `persisteVolumeReclaimPolicy: Retain`
  - `persisteVolumeReclaimPolicy: Delete`
  - `persisteVolumeReclaimPolicy: Recycle`

```yaml
spec:
  container:
  - name: mypod
    image: nginx
  volumes:
  - name: myvolume
    persistentVolumeClaim:
      claimName: myclaim
```

## Storage Class:
- Object that can provision storage like Google Cloud automatically and attach it to the pod
- We use `storageClasses` to link pvc
  - `persisteVolumeReclaimPolicy: Retain`
- If we are using StorageClass the **pv is no longer needed**
- PV is automatically created by StorageClass
- You can provision type of storage like standard, ssd, ssd with replication etc.

### Lab Learning
- The provisioner that has `no-provisioner` in the name is not dynamic provisioning.