# Container Orchastration

Let's disect the tools and tech in three sections and look at them. We will deep dive in each in further sections

## Orchastration
- Docker
- Kuberenetes

## Container Runtime Interface:
Used for push & pull image, supervise containers and much more
- ContainerD
- CRI-O

## Open Conatiner Initiative (OCI) runtime
These help us create and run containers, Difference between native & virtual is **Isolation**
- Native:
    - runC
    - Crun
- Virtual:
    - gViso
    - nabla-containers
    - kata-containers