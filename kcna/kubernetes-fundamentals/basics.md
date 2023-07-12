# Basics

It is really essential to understand some basics components before jumping into kubeneretes.

## Virtual Machines (VMs):
Virtual machines do not make the best use space. Aps are not isolated which could cause config conflits, security problems or resource hogging.

## Containers:
containers allow you to run multiple apps which are virtually isolated from each other

## Microservices:
- Multiple apps which are responsible for one thing
- Functionality are ***isolated and stateless***

## Kubernetes:
Kubenerets is an open source container orchestration system for deployment scaling and management.
- Unique component is pod
- A pod is a group of one or more containers with shared storage and network resources & other settings
- K8s is ideal for microservice architecture