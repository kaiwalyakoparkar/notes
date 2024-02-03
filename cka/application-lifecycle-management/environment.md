# Environment

```yaml
spec:
  containers:
  - name: myapp
    image: myapp:latest
    env:
    - name: APP_COLOR
      value: pink
```

- But we generally put env's in configmaps or secrets.