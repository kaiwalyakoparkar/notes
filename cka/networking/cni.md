# Container Networking Interface (CNI)

- In kubelet.service you can ind out type of network plugin, bind directory & conf directory
  ```bash
  --network-plugin=cni
  --cni-conf-dir=/opt/cni/net.d
  --cni-bin-dir=/opt/cni/bin
  ```
- You can view this using:
  ```bash
  ps -aux | grep kubelet
  ```

## Learning Lab
- Has CNI Plugins on host `/opt/cni/bin`
- Find CNI plugin configured `/etc/cni/net.d`

## Service Networking

- You can get ip allocations of pods from weave pod by checking its logs
- IP range of service is mentioned in kube-apiserver config ile under `--service-cluster-ip-range=x.xx.x`
