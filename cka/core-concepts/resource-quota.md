# Resource Quota
You can set resources quota for a namespace.

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
    name: pods-low
spec:
    hard:
        cpu: "5"
        memory: 10Gi
        pods: "10"
```