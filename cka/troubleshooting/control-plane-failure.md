# Control Plane Failure

1. If kubeadm check pods in kube-system namespace.
2. If deployed as service then check the service workings
  - 
    ```bash
    service apiserver status
    ```
  -
    ```bash
    service kube-controller-manager status
    ```
  -
    ```bash
    service kube-scheduler status
    ```
  -
    ```bash
    service kubelet status
    ```
  -
    ```bash
    service kube-proxy status
    ```
3. Check logs of control plane compnents
  - If kubeadm use logs
    ```bash
    kubectl logs <name> -n kube-system
    ```
  - If deployed as service use
    ```bash
    sudo journalctl -u <name>
    ```
  - If error with certificates, check volumes, volumeMounts & direct volumes