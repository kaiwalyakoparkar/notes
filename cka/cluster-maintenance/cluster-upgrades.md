# Cluster Upgrades:

- No other components should have version higher than kube-apiserver.
- Kubectl can have version higher than kube-apiserver.
- IF your cluster is at `v1.10.0` and latest version release is `v1.13.0` then it would be correct time to upgrade.
- For upgrading we don't directly jump to newer version
- `v1.10.0` -> `v1.11.0` -> `v1.12.0` -> `v1.13.0`

- ***Upgrading  cluster involves 2 major steps***
  - Upgrading Master Node
  - Upgrading Worker Node

- ***kubeadm Upgrade***
  - `kubeadm upgrade plan`
  - We must manually upgrade kubnelet on each node as kubeadm doesn't do that

- ***Kubeadm command chain: [Master Node]***
  - `apt-get upgrade -y kubeadm=1.12:0-00` - new version instead of 1.12
  - `kubeadm upgrade apply v1.12.0`
  - `apt-get upgrade -y kubelet=1.12.0-00`
  - `systemctl restart kubelet`

- ***Kubeadm command chain: [Worker Node]***
  - `kubectl drain node1`
  - `apt-get upgrade -y kubeadm=1.12.0-00`
  - `apt-get upgrade -y kubelet=1.12.0-00`
  - `kubeadm upgrade node config --kubelet-version v1.12.0`
  - `systemctl restart kubelet`
  - `kubectl uncordon node1`

- Kubeadm version is always similar to kubernetes lates.
- Usually update kubeadm first
- Then drain the nodes etc. & proceed forward.