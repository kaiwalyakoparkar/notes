# Docker & Cluster Networking

## Docker Networking

```bash
docker network ls
```

## Cluster Networking

- ETCD: 2379 port
- kube-api: 6443 port
- kubelet: 10250 port
- kube-scheduler: 10251 port
- kube-controller-manager: 10252 port
- services: 30000-32767 port

### Commands

- 
  ```bash
  ip link
  ```
- 
  ```bash
  ip addr
  ```
- 
  ```bash
  ip addr add 192.xx.xx/x dev eth0
  ```
- 
  ```bash
  ip route
  ```
- 
  ```bash
  ip route add xx.xx.xx via xx.xx.xx
  ```
- 
  ```bash
  cat /proc/sys/net/ipv4/ip_forward
  ```
- 
  ```bash
  arp
  ```
- 
  ```bash
  netstat -plnt
  ```
- 
  ```bash
  route
  ```

### Lab Learning

- 
  ```bash
  ip a | grep -B2 <node-ip-address>
  ```
- Get Mac Address
  ```bash
  ip link show eth0
  ```
- Check ip corersponding with network interface, select that
  ```bash
  ip address
  ```
- Shows all bridges on the host
  ```bash
  ip address show type bridge
  ```
- 
  ```bash
  netstat -nlp | grep i <name>
  ```

## Pod Networking
1. Kubelet
2. Checks location of the script
  ```bash
  --cni-conf-dir=/etc/cni/net.d
  ```
3. Finds the script
  ```bash
  --cni-bin-dir=/opt/cni/bin
  ```
4. Executes the snippet
  ```bash
  ./net-script.sh add<container> <namespace>
  ```