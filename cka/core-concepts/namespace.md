# Namespace
- Default: We generally create stuff here
- kube-system: Has k8s specific stuff
- kube-public: Resource made available to all

- DNS record for namespaces: `service-name.ns-name.svc.cluster.local`

## Switch Namespace:
- `kubectl config set-context $(kubectl current-context) --namespace=<ns-name>`

## Commands/ Flags
- `--all-namespace`
- `-A`