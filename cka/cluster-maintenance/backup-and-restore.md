# Backup and Restore

- Backup Candidates
  - Resource configuration
  - ETCD cluster
  - Persistent Volumes


## Resource Configuration

- We can easily get the configs declared declaratively in yaml format.
- If you create it imperatively & do not document it then it would be hard to redeploy if something goes wrong.
- Hence we query the `kube-apiserver` and save all resources configs for all objects created on server
- `kubectl get all -A -o yaml > back.yaml`
- We use tools like velero (ARK) that covers every resources excluded by above commands