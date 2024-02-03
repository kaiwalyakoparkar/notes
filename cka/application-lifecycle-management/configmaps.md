# Configmaps

- Saves the environment data in key-value format
- 2 steps are involved here:
  - create configmap
  - Inject into pod

## Create Configmap

```yaml
kubectl create configmap <configmap-name> --from-literal=<key>=<value>
```
- Declarative Approach:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: <configmap-name>
data:
  APP_COLOR: pink
  APP_MODE: prod
```

## Injecting Into Pod

```yaml
spec:
  containers:
  - name: myapp
    envFrom:
    - configMapRef:
        name: <configmap-name>
```