# Basics

## Kubernetes Architecture
- Master Node
    - ETCD cluster
    - Kube Apiserver
    - Kube Controller Manager
    - Kube Scheduler
- Worker Node
    - Kubelet
    - Kube proxy
    - Container Runtime Engine

## Command line tools for containers
- CTR
    - Purpose: Debugger
    - Conmmunity: ContainerD
    - Works with: ContainerD
- nerdctl
    - Purpose: General purpose
    - Community: ContainerD
    - Works with: ContainerD
- Crictl
    - Purpose: Debugging
    - Community: Kubernetes
    - Works with: All CRI compatible runtimes