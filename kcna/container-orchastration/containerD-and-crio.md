# ContainerD and Cri-O

## ContainerD:
- ContainerD is an industry standard container runtime with emphasis on simplicity, robustness and portability
- This includes Docker's functionality for executing containers, low-level storage & managing image transfers.
- ContainerD makes it easier for projects like K8s to access the low-level "Docker" elements they need
- Images built with Docker aren't really "Docker image"
- Images are built in the standardized OCI format.

![ContainerD logo](https://containerd.io/img/logos/main-logo.png)

## CRI-O
- Alternative to using Docker
- It supports runc & kata containers as container runtimes

![CRI-O logo](https://cncf-branding.netlify.app/img/projects/crio/horizontal/color/crio-horizontal-color.png)