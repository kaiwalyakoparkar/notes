# Detailed Concepts

This segment consits of detailed bits about important concepts and components of kubernetes

## Endpoints:
Endpoints track ip addresses of the pods assigned to the kubernetes service
```bash
kubectl get endpoint
```

## Endpoint slices:
This breaks up end points into smaller manageble segments. Each slice has limit of 100 pods. Essential while solving scaling problems

## Jobs:
A job creates one or more pods and will continue to retry execution of the pods until a specified number of them successfully terminate.
```bash
kubectl create job hello --image=busybox -- echo "Hello World"
```

# Cron Jobs:
It is a job that executes based on repeating schedule.

```bash
kubectl create job hello --schedule="*\1 * * * *" --image=busybox -- echo "Hello World"
```

## Selectors:
They are the way of selecting one or more kubernetes objects
1. Label selectors
2. Field selectors
3. Node selectors

K8s objects like `services` and `replicasets` will traget  pods based on label selectors.

```bash
kubectl get pods --show-labels
```

## Annotations:
Kubernetes annotations allow you to watch arbitory non-identifying metadata to objects. Often used by **Ingress**

## RPC (Remote procedure call):
- It enables preogram to communicate with another program on a remote machine without knowing its remote.
- RPC is a framework of communication in distributed systems.

## gRPC
```💡 Think of this as method instead of REST or GraphQL```

- gRPC is a modern open source high performance RPC. 
- Kuberenetes uses gRPC for Pod communication

## Kubelet:
- It is responsible for pod internal API communication via the API server.
- Node agent that runs on all nodes. Kubelet performs
    - Watchs pod changes
    - Configures container runtime
    - Pull images
    - Create Namespaces
    - Run containers

## Kubectl:
- `kubectl [command][TYPE][Name][Flags]`
- Commands: 
    - apply
    - get
    - log
    - describe
    - exec
- Type:
    - deploy
    - pods
    - ns
    - pc
    - pvc
    - secret
- Name:
    - case_sensitvie_name
- Flags:
    - different for each command
    - starts with `--`

## Services:
Ip adresses of pods are ephemeral (temporary) hence we need services.

## API Server:
- Exposes an HTTP API that lets end users, access different parts of your cluster and external components with one another.
- Let's you query & manipulate state of API objects in k8s
- Designed to scale horizontally.

## Deployments:
Defalult deployment controller can be swapped out for other deployments tools eg: ArgoCD, Flux, Jenkins X

## Replica Sets:
- ReplicaSet is a way to maintain a desired amount of redundant pods (replicas) to provide guraanteed availability.
- Horizontal pod autoscalar (HPA) can be used to autoscale a replicaset

## Stateless:
- ReplicaSet is used for implementing
- Send request to any server, it doesn't matter

## Stateful:
- StatefulSet is used for implementing
- Store session data in memory on VM

## StatefulSet:
- A unique name and address is provided.
- Original index number assigned to each pod.
- Persistent volume is attached with a persistent link from pod to storage.
- StatefulSet will always start in the same order, and terminate in reverse order.
