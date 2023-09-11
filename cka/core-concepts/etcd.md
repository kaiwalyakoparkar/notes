# ETCD
- Command line tool: `etcdctl`
- `etcdctl` set key value
- Every information you get after running kubectl comes from etcd store
- ETCD manages information of 
    - Nodes
    - Pods
    - Configs
    - Secrets
    - Accounts
    - Roles
    - Bindings, etc
- 2389 is default port on which etcd listens

## ETCD in HA environment
- It is essential that different etcd instances spread across different master nodes
- It is important that etcd stores know about each other with right configuration using parameters
- `--initial-cluster` is where you specify instances of different etcd service

## ETCD commands:
- `etcdctl` can interact with ETCD server using 2 & version 3
- Default is set to version 2
- Version 2 supports commands
    - `etcdctl backup`
    - `etcdctl cluster-health`
    - `etcdctl mkdir`
    - `etcdctl get`
    - `etcdctl put`
- To set right version of API. Set the environment variable `export ETCDCTL_API=3`
- Certificates for `etcdctl` to authenticate etcdctl api server can be located at 
```bash
--cacert /etc/kubernetes/pki/etcd/ca.cert
--cert /etc/kubernetes/pki/etcd/server.cert
--key /etc/kubernets/pki/server.key
```