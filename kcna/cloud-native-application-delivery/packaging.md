# Helm and IaaC:

## Helm:
- Helm is package manager for K8s
- Helm is broadly composed of 3 components:
    - Chart: Contains all necessary resource definitions to run app, tool on K8s cluster
    - Repository: The palce where charts can be collected and shared
    - Released: An intence of a chart running in K8s cluster
- Artifacthub is where we find and public helm charts

## Kustomize:
- Maybe alternative to Helm
- It provides more flexibility when writing
- Kustomize it's built into kubectl
- Kustomize file defines what will be overwritten in the base component.

## Infrastructure as a Code (IaaC):
- Script to automate, create, update or destory cloud infrastructure
- IaaC is blueprint of your infrastructure
- IaaC allows easy share, version or inventory your cloud infrastructure

### Popular Infrastructure
- Declarative:
    - Terraform
    - Azure blueprint
    - Cloudformation
- Imperative:
    - AWS cloud development kit
    - Pulumi

## IaaC for Kubernetes:
- Managin Infra _of the cluster_:
    - Terraform
- Managing Infra _in the cluster_:
    - Helm
