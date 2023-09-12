# K8s Objects
## Pod
1. `kubectl describe pod <pod_name>`
    - Tells you status of containers
    - Number of containers
    - Types of containers
    - Logs if containers fails
2. `kubectl run <pod_name> --image=<image_name> --dry-run=client -o yaml > file.yaml`
    - Create yaml file for the pod
    - We can now implement by using `kubectl apply -f file.yaml`
3. `kubectl get pods -o wide`
    - Gives more info about pod like nodes it is running on

## Replicaset
1. `kubectl edit rs <name-of-replicaset>`
    - Lets you edit yaml of already created replicasets
2. `kubectl scale rs/<name-of-replicasets> --replicas=<rs-number>`
    - Lets you scale thereplicas without going & editing yaml

## ReplicaSet commands
- `kubectl create -f rs.yaml`
- `kubectl get replicaset`
- `kubectl delete rs my-replicaset`
- `kubectl replace -f replicaset-def.yaml`
- `kubectl scale rs my-rs --replicas=6`

## Deployment
`kubectl get all`
    - Shows deployment
    - Shows replicasets
    - Shows pods