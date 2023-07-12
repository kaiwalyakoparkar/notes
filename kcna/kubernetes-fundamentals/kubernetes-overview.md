# Kubernetes Overview

Kubenerets is an open source container orchestration system for deployment scaling and management. K8s is ideal for microservice architecture

This page contains one line overview of concepts to quick recap kubernetes :)

![Phoenixnap image](https://phoenixnap.com/kb/wp-content/uploads/2021/04/full-kubernetes-model-architecture.png)

(Image by: pheonixnap.com)

## Cluster
A logical grouping of all components within a cluster

## Namespace:
A named logical grouping of Kubernetes component within cluster

## Node:
VIrtual Machine or underlying server. There are 2 types of node in a cluster.
1. Control Plane (Manages Worker Nodes):
    - Consists of API Server
    - Scheduler
    - Control Manager
    - etcd
    - Kubelet
    - CoreDNS
2. Worker Nodes (Workload run here)
    - Kubelet
    - Kubeproxy
    - Container Runtime
    - Pods & Containers

## Pod:
Smallest unit in k8s. It is abstraction over **containers**.

## Service:
Used to allocate static IP addresses and DNS names for set of pods

## Ingress:
Translates HTTP/s rules to point to service.

## API Server:
Helps users interact with k8s cluster using `kubectl` or by sending HTTP requests.

## Kubelet:
Helps interact with nodes via API server. ***Present on all nodes***

## Kubectl:
Command line terminal for k8s

## Cloud Controller Manager:
Allows you to link a cloud service provider

## Controller Manager:
Watches and changes current state back to the desired state.

## Scheduler:
Determines where to place pods on nodes

## Kubeproxy:
Provides routing & filtering rules for traffic to pods

## Network Policy:
Acts as a virtual firewall bewtween namespaces, pods, nodes, etc

## ConfigMap:
Used to store ***Non Confidential*** data into key value pair.

## Secret:
Stores sensitive data like passwords, tokens or key.

## Volumes:
Mounting storage to store the data for application to use and preserve.

## Replica Set:
Maintain a stable set of replica pods running at given time.

## Deployment:
It is a blueprint for a pod.

## In-Tree:
Plugins and components or functionality that are provided by default or resides in main repository

## Out-Tree:
Plugins and component or functionality that must be installed manually that replaces default behaviour.