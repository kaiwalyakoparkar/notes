# Resource Requests [Pod]

```yaml
spec:
    containers:
    - name: myapp
        image: myapp:latest
        resources:
            requests:
                memory: "64Mi"
                cpu: "2"
```

# Resource Limits [Pod]

```yaml
spec:
    containers:
    - name: myapp
        image: myapp:latest
        resources:
            request:
                memory: "1Gi"
                cpu: "1"
            limits:
                memory: "2Gi"
                cpu: "2"
```

- Containers can't user more CPU than it's limit
- A container can use more memory than its limits

# Limit Range

- Helps us to set a default limit or request.

```yaml
spec:
    limits:
    - default:
        cpu: "500m"
      defaultRequest:
        cpu: "500m"
      max:
        cpu: "1"
      min:
        cpu: "100m"
      type: Container
```

# Resource Quotas

- These are used to define and restrict how much membery & cpu can all pods utilize.
- Max resource limits are mentioned.

## Lab Learning [Resources]

- We can't change pod resources during its execution hence on changes are saved in `/temp/` directory.
- We can use `kubectl replace --force -f </temp/location>` it will terminate running pod and create new one.

# Static Pods

- The pods created by kubelet without intervention from kube-apiserver are called as static pods.
- Manifests for pods are saved in `/etc/kubernetes/manifests`.
- We can't create deployments, replicasets, services using this.

## Lab Learnings [Static Pods]

- Static pods are visible by `get pods` command.
- It will have `node-name` after it's name, that's how you find static pods
- eg: `kube-apiserver-controlplane` - controlplane is the node name.
- To delete pod, you have to delete manifest file in location.
- Similarly update it.
- To delete static pod in different node
	- ssh into node
	- go to `/var/lib/kubelet/config.yaml`
	- find `staticPodPath`
	- Go to the path and you'll find static pod manifest.
	- Delete it using `rm` command.

# Manual Schedules

- The scheduler config can be found at `/etc/kuberenetes/config/...yml`
- If we have multiple mast nodes then only 1 scheduler configuration can run at a time.
- We can use `leaderElection` & `leaderElect=true` to define leader in multiple master scenario.
- We can specify what scheduler picks up the pod using `schedulerName:<name-of-scheduler>`
- `kubectl logs <scheduler-name> -n ns`
- `kubectl get events`

## Stages of Scheduling
- Scheduling Queue
- Filtering
- Scoring
- Binding