# Secrets

- Secrets are used to store sensitive data
- Secrets files looks similar to config files
- Save the encoded format
```bash
echo -n "secret-key" | base64
```
- Do view the secret decode it
```bash
echo -n "secret-key" | base64 --decode
```

## Injecting Secret Into Files

```yaml
spec:
  containers:
  - name: myapp
    envFrom:
    - secretRef:
        name: <secret-name>
```

## Important Note for Secrets

- Secrets are **not encrypted**. Only encoded.
- Secrets are not encrypted in etcd.

