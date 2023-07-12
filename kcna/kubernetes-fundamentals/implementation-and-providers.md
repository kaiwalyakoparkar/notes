# Implementation and providers

## Minikube:
- Used to create single node clusters.
- Minikube is running VM -> running a control-plane and work processes with docker as the container layer

![Minikube logo](https://www.couchbase.com/wp-content/original-assets/september-2016/minikube---rapid-dev--testing-for-kubernetes/minikube-logo-1024x290.jpg)

## K3s and K3D:
- K3s is a lightweight tool to run production - level workloads for 
    - Low resourced
    - Remotely located IOT & Edge devices
    - Bare metal
    - Created by Rancher
    - Sandbox CNCF Project
- K3s does not use Kubelet, it uses host machine & its mechanism to run containers.
- K3s uses kube-proxy to proxy the network connection of the nodes
    - Whereas, *K8s uses kube-proxy to proxy the network connection of **individual container***
- K3s has more security deployment than K8s
- K3D is lightweight wrapper that runs k3s in a docker container.

![K3s logo](https://docs.k3s.io/img/k3s-logo-dark.svg)

## Kind:
- Kind is primarily designed to test kuberenetes
- Kind helps run Kubernetes clusters locall and in CI pipelines using Docker container as "nodes"

![Kind logo](https://d33wubrfki0l68.cloudfront.net/d0c94836ab5b896f29728f3c4798054539303799/9f948/logo/logo.png)

## MicroK8s:
- MicroK8s is created by Canonical and is installed using snap.
```bash
sudo snap install microk8s --classic
```
- K8s distribution designed to run fast, self healing, and highly available clusters
- Optimized for quick and easy installations of single and multi node clusters on OS (as long as it has snap)
- Ideal for running k8s in cloud, local development environment, Edge and IoT devices
- MicroK8s is modular in design can enable addons for exactly what you need.

![MicroK8s logo](https://global.discourse-cdn.com/business6/uploads/kubernetes/original/2X/5/52c2e57feb961611de65abf267208fa8a957f5f5.png)

## In-short:
1. **Minikube**: Development use
2. **Kind**: Development use
3. **K3s & K3D**: Production use
4. **MicroK8s**: Production use

## Managed Kubernetes Providers:
- Google Kubernetes
- Amazon Elastic Kuberenetes Service (EKS)
- Azure Kubernetes Service (AKS)
- IBM Cloud Kuberentes Service.
- Oracle container engine for kubernetes
- DigitalOcean Kubernetes (DoKs)
- Civo (Focused on just K8s)

## Management Layers
Allows you to extend your control plane to multiple platform
- Weave K8s platform (WKP)
- Rafey
- VMWare Tanzu
- Azure Arc
- Google Antlos
- Platform 9
- RedHat OpenShift:
    - Plaform as a service for K8s
    - Extended kubectl (Oc Cli)
- Rancher Kubernetes Engine:
    - Runs within docker container
    - Works on bare metal