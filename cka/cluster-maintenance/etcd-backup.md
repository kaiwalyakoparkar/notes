# ETCD Backup

- We specify where the data will be store during configuration of ETCD `--data=dor=/var/lib/etcd`
- To use the backup mechanism ETCD needs to have `ETCDCTL_API` version to 3. You can configure that by running `export ETCDCTL_API=3`
- Create snapshot of the data `etcdctl snapshot save file-name.db`
  - Saved in current directory, else provide path to save it at seperate location
- View the status of backup using `etcdctl status file-name.db`
- For restoring, first stop api-server service: `service kube-apiserver stop`
- Restore the state of etcd and ssave new state to a directory: `etcdctl snapshot restore file.db --data-dir /var/lib/etcd-from-backup`
- Configure the etcd configuration to utilize the new data configuration file at `--data-dir=/var/lib/etcd-from-backup`
- Run: `systemctl daemon-reload`
- Run: `service etcd restart`
- Run: `service kube-apiserver start`
- With all etcdctl commands remember to specify `--endpoints=`, `--cacert=`, `--cert=`, `--key=`

## Lab Learning [ETCD backup & restore]

- Stacker ETCD means - etcd pod inside cluster
- Get version of etcd by running the etcd pod's description and its image version
- `--listen-client-urls` provides address that can reach ETCD cluster.
- Server certificates files are located at `/etc/kubernetes/pki/etcd/` (ETCD server certificate)
- CA certificate are loacated at `/etc/kubernetes/pki/etcd`
- ```bash
  ETCDCTL_API=3 etcdctl \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  snapshot save /location/name.db
  ```
- Make Restore
  ```bash
  ETCDCTL_API=3 etcdctl \
  snapsthot restore --data-dir=/new/dir/ /location/name.db
  ```
- Change the path in volumes to `/new/dir`

```yaml
volumes:
- hostPath:
    path: /new/dir
    type: DirectoryOrCreate
  name: etcd-data
```
This will be present in etcd pod aml file in `/etc/kubernetes/manifests/etcd.yaml`

## Multicluster Format

- Get clusters a node can access `kubectl config get-clusters`
- `kubectl config view`
- Shift context between clusters `kubectl config use-context <cluster-name>`
- If the etcd pod is **found on controlplane** in kube-system namespace then **etcd is stacked**
- If the etcd pod is **not found on controlplane** and has entry in kube-apiserver the `etcd is external`
- You can locate the etcd server if or location at `--etcd-server` in the kube-apiserver pod description.
- Data directory for etcd can be found using `--data-dir` in etcd pod or volume spec.
- To find data directory of an external etcd-server:
  - ```
    ssh etcd-server
    ```
  - ```
    ps -ef | grep -i etcd
    ```

- Taking a snapshot when in multicluster.
  - `ssh controlplane`
  - `etcd snapshot save a.db [--flags endpoints, cacert, cert, key]`
  - `exit`
  - `scp controlplane:/root/location/a.db /opt/` - /opt/ is destination
- Wee are copying the snapshot out of cluster into node managing these clusters.

## Restoring Snapshot in external ETCD:

- Cpy backup file from node to external etcd server:
  ```
  scp /location/ad.db etcd-server:/root/
  ```
- 
  ```
  ssh etcd-server
  ```
- Perform restore:
  ```
  etcdctl snapshot restore file.db --data-dir=/var/lib/etcd-new
  ```
- Verifying ownership
  ```
  ls -la /var/lib/
  ```
  ```
  chown -R etcd:etcd new-dir/
  ```
- 
  ```
  vim /etc/systemd/system/etcd.service
  ```
  [Change --data-dir=/new-dir]
- 
  ```
  systemctl daemon-reload
  ```
- 
  ```
  systemctl restart etcd
  ```
- 
  ```
  systemctl status etcd
  ```
- 
  ```
  exit
  ```
- 
  ```
  kubectl get all -n critical
  ```

Parent: 
```
scp /parentnode/ etcd-server:/root/
```
ETCD:
```
snapshot restore --data-dir=new-loc
```
ETCD:
```
ls -la /var/lib/
```
ETCD:
```
chown -R etcd:etcd /var/lib/new-loc
```
ETCD:
```
vim /etc/systemd/system/etcd.service
```
ETCD:
```
--data-dir=/var/lib/new-loc
```
ETCD:
```
systemctl restart etcd
```
ETCD:
```
systemctl restart etcd
```
Parent:
```
kubectl delete pod controller scheduler
```
Parent:
```
get controller & scheduler back-up again
```