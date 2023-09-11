# K8s Componenets 
## Kube-apiserver
1. Authenticate user
2. Validate request
3. Retrieve data
4. Update ETCD
5. Scheduler
6. Kubelet

- In `kube-apiserver` service we define location of etcd server `--etcd-server=https://127.0.0.1:2379`
- View api-server option
```bash
cat /etc/kubernetes/manifests/kube-apiserver.yaml
```
```bash
cat /etc/systemd/system/kube-apiserver.service
```
```bash
ps -aux | grep kube-apiserver
```

## Kube-controller manager
- Watch Status
- Remediate situation
- Node Monitor Period = 5s
- Node Monitor Grace Period = 40s
- Pod Eviction Timeout = 5m

## Different Controllers in kube control manager
- Node Controller
- PV-Binder Controller
- Replication Controller
- Service account controller
- Stateful-Set
- Replicaset
- CronJob
- Job Controller
- PV Protection Controller
- Deployment Controller
- Namespace Controller
- Endpoint Controller

## Kube Scheduler:
1. Filter Nodes
2. Rank Nodes

## Kubelet:
1. Register Node
2. Create Pods
3. Monitor node & Pods

- With the command, kubeadm doesn't deploy kubelet by default

## Kube-proxy:
- Deployed as daemonset on cluster