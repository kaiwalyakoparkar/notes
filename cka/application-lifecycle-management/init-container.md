# Init Container

- Container runs at start when pod is created
- Used to fetch and configure info for main application to use.

```yaml
spec:
  containers:
  - name: myapp
  initContainers:
  - name: init-service
```
