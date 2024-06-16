# Designing

- Ask following questinos before designing
1. Purpose:
  - Education (Minikube)
  - Development & Testing (Multi node)
  - Hosting production Apps
2. Cloud on OnPrem
3. Workloads
  - How many?
  - What kind?
    - Web
    - Big data/Analytics
  - Application Resource Requirements
    - CPU intensive
    - Memory intensive
  - Traffic
    - Heavy Traffic
    - Burst Traffic
  
## Hosting Production Application

- High availability multi node cluster with multiple master node.
- Kubeadm or GCP or Kops oR AWS
- Upto 5000 nodes
- Upto 150000 pods in the cluster
- Upto 300000 total containers

## Cloud or OnPrem

- Use Kubeadm or on-pre 
- GKE for GCP
- Kops for AWS
- Azure Kubernetes Service (AKS) for Azure

## Storage

- High performance SSD Backed storage
- Multiple concurrent connections network based storage
- Persistent shared volumes for shared access accros multple pods
- Lable nodes with specific disk type
- Use node selectors to assign apps to node with specific disk size

## Nodes

- Virtual or Physical Machines
- Minimum of 4 node cluster
- Master vs worker nodes
- Linux x86_64 architecture
- Master nodes can host workloads

## Configure HA

### kube-controller-manager

```yaml
--leader-elect true
--leader-elect-lease-duration 15s
--leader-elect-renew-deadline 10s
--leader-elect-retry-period 2s
```

### ETCD

- Stacked Topology
  - Resides inside master node
  - Easier to setup
  - Easier to manage
  - Fewer serves
  - Risk during failures
- External Topology
  - Resides outside master node
  - Less Risky
  - Harder to setup
  - More servers
- In distributed architecture, only one etcd node is responsible to write data
- While you can read the data from any etcd instance
- Leader election in ETCD is done using RAFT protocol (Random Timers used)
- For master nodes to bear fault tolerance it is always preferred odd number of managers available (Over 3)
- 
  ```bash
  export ETCDCTL_API=3
  ```
- 
  ```bash
  etcdctl put name john
  ```
- 
  ```bash
  etcdctl get name
  ```
- 
  ```bash
  etcdctl get / --prefix --keys-only
  ```