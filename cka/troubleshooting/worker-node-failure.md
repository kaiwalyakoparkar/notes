# Worker Node Failure

- When worker node is unable to communicate with master the flags are set to `unknown`
- Use `top` and `df -h` commands to check CPU usage etc
- Check `kubelet`
- Check kubelet certificates and make sure they are not expired `/var/lib/kubelet/<name>.crt`
- Port error `/etc/kubernetes/kubelet.conf`