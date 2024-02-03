# Taints and Tolerations

- Taints are set of Nodes
- Tolerations are set of POds
- Taint a Node:
```
kubectl taint nodes node-name key=value:taint-effect
```
- `taint-effect` is what happens to pod if they don't tolerate taint
- taint-effects:
    - NoSchedule
    - PreferNoSchedule
    - NoExecute
- Toleartion for pod:
```
kubectl taint node node1 blue=app:NoSchedule
```
- So toleration can be added using 
```yaml
spec:
    tolerations:
    - key: "blue"
      operator: "Equal"
      value: "app"
      effect: "NoSchedule"
```