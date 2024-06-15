# Security Contexts

- If we configure security at pod level then all the contianers get the configurations
- If we configure the container then it will override the pod's security settings on pod
- Add security context to pod
  ```yaml
  spec:
    containers:
    - name: nginx
      image: nginx
    - name: busybox
      image: busybox
    securityContext:
      runAsUser: <name>
      capabilities:
        add: ["MAC_ADMIN"]
  ```
- 
  ```bash
  kubectl exec <pod-name> -- whoami
  ```