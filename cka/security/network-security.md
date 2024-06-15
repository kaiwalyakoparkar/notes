# Network Security

- By default the rule is "All Allow" so all pods can access all pods
- Network policies allow you to restrict the traffic coming or going from the pod
- 
  ```yaml
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          name: <name>
    ports:
    - protocol: TCP
      port: 3306
  ```
- 
  ```yaml
  apiVersion: networking.k8s.io/v1
  kind: NetworkPolicy
  ```