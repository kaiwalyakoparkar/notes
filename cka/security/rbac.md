# RBAC (Role Based Access Control)

- Create 2 definition files, role and role binding.
- 
  ```bash
  kubectl get roles
  ```
- 
  ```bash
  kubectl get rolebindings
  ```
- 
  ```bash
  kubectl describe role <role-name>
  ```
- 
  ```bash
  kubectl auth can-i delete pod
  ```
- 
  ```bash
  kubectl auth can-i create pods --as dev-user
  ```

## ClusterRole & ClusterRoleBinding

- For cluster scoped resources
- We can use this for namespced resources as well to grant user access for pods over all namespaces

## Service Accounts

- Can be used by an application to comunicate with kubernetes cluster. eg [Prometheus, Jenkins]
- 
  ```bash
  kubectl create serviceaccount <service-account-name>
  ```
- 
  ```bash
  kubectl get serviceaccount
  ```
- Add custom service account name using `serviceAccountName: <name>` in pod definition file.
- K8s automatically mounts service accounts on pods, we can choose not to using `automountServiceAccountToken: false` in pod definition file.
- We gt token that can be decoded and used to call kube-apiserer
  ```bash
  kubectl exec -it <name of pod> ls /service/account/token/location
  ```
- With newer version it no longer creates automatic token for service account. To create token:
  ```bash
  kubectl create token <service-account>
  ```

## Image Security:
- We can pass private repository name as it is in the image section of pod definition
- To authenticate for private images we need secret named docker-registry
- 
  ```bash
  kubectl create secret docker-registry regcred \
  --docker-server=<private>\
  --docker-username=<username>\
  --docker-password=<password>\
  --docker-email=<registry-email>
  ```
-  In pod definition link this secret as follows undere spec section with containers.
  ```yaml
  spec:
    imagePullSecrets:
    - name: regcred
  ```

