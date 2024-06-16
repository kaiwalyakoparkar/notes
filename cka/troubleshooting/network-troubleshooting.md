# Network Troubleshooting

## `service kubelet restart`

- Port 53 is used for DNS resolution
- Check CoreDNS pod status & see if network plugin installed
- Remember path `/run/systemd/resolve/resolv.conf` for using resolv.conf

## `journalctl -u kubelet`

- Check Kube-proxy logs
- Check conigmap
- Configmap should match kube-proxy daemonset