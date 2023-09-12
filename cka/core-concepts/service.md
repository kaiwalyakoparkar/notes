# Services

One of the essential commands that might come handy are
```bash
kubectl expose pod <pod-name> --port=<number> --name=<service-name>
```
Following create service with same name as pod and exposes it
```bash
kubectl run <pod-name> --image=<image-name> --port=<number> --expose=true
```