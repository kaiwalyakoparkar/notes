# Commands & Arguments

```yaml
spec:
  containers:
  - name: myapp
    image: myapp:latest
    command: ["sleep 2.0"] # Entrypoint in docker
    args: ["10"] ## Command in docker
```