# CoreDNS

- Configured at `/etc/coredns/Corefile`
- We can edit this using its configmap object
- Kubelet config file has cluster DNS ip in it `/var/lib/kubelet/config.yaml`

## Nginx: (Ingress)

- Need Deployment defition file
- Needs configmap (Empty is okay)
- Mention configmap in args
- Mention ports
- Declare service
- Create ServiceAccount
- Resource file with `kind: Ingress`
- 
  ```yaml
  spec:
    backend:
      serviceName: nginx
      servicePort: 80
  ```
- 
  ```bash
  kubectl get ingress
  ```
- The above yaml is for single simple service forward
- For multiple service routing we need `rules`
- 
  ```yaml
  spec:
    rules:
    - http:
        paths:
        - path: /url
          backend:
            name: nginx
            port:
              number: 80
  ```