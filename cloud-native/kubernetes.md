# Kubernetes

## History

![](https://media.giphy.com/media/9V71czzFLwBNE0O8EV/giphy.gif)

### - Bare metal servers
It is typically a single computer server which is used by only one consumer or tenet. Each server offered for rental is a distinct physical piece of hardware that is a functional server on its own.
### - Virtual Machine
As you might have already used virtual machines for trying out differnt operating systems. Virtual machines helps your softwares to share same physical resources instead of seperate physical resources for each software which would increase the cost drastically.
### - Containers
Containers are similar to virtual machines conceptually. But the key factor is that containers run the program in isolated environments.

## Monolithic v/s Microservices
There are multiple resources revolving around monolithic and microservice so I will try to make it as simpler and shorter as possible (because that is not really main scope of this blog and would need a dedicated article on itself),
So let's say you have an application which has frontend, backend, database etc and you containerize your entire application in one container then that is called as a monolithic architecture. So if your container goes down your entire instance of that application goes down. Now the reverse is that you containerize each part of your application and connect them with each other, now this each containerized part of application is called as microservice. *(See the image below for better understanding)*

![Monolitic v/s microservices image](https://i.imgur.com/0wyC8JU.png)


## What is Orchestration?
Orchestration has multiple definitions. You can think of it as a automation process which helps us in deploying and managing the application. So the orchestrator will keep looking for anything wrong with your deployment and try to self heal, scale to keep your production damages to it's lowest. You can picture it as the orchestrator in an orchestra who is responsible to create a melody and monitor it continuously.

![Orchestrator](https://i.imgur.com/3Av5QBg.png)


## What is Kubernetes?
Kubernetes also known as k8s (Fun fact: It is called k8s becuase it has 8 letters between `K` & `S` in word `Kubernetes`) is widely termed as Container orchestrator but Kubernetes is not just container orchestrator which means it helps you orchestrate the containers and provide additional features like 
- Deploy your application
- Enable zero downtime updates (Also called rolling updates)
- Helps scale your application dynamically with increasing or decreasing traffic
- Self heals the containers and other services.
- Run it on our own machine/cloude
- Run it on public cloud providers
- Helps migrate from one cloud provide to other
- It can also replicate services, scale those services
- You can also use Volumes (Much more about volumes in upcoming blogs)
- One of the prominent feature is load balencing

There are many more such features provided by Kubernetes apart from once mentioned above that seperates it from being just the 'container orchestrator'.

## Kubernetes Cluster

Cluster is the outer most box which holds everthing. Cluster is simply a collection of Control Plane and Worker nodes. *(Refer the diagram below with the explaination in the blog to build good intuition of the architecture)*

![K8s Cluster](https://i.imgur.com/CrV5lgs.png)

### KubeCtl (CLI)
This is a command line tool provided to us so we can communicate with our control plane do apply and do the changes. Optionally if you don't want to work with cli there are also few gui provided you can take a look into. KubeCtl must be installed on your local machine in order to talk to the API server in the control plane.

### Control Plane

1) **API Server:** All the communication will happen via api server. It listens to requests on `HTTPS` and port `443`

2) **Controller Manager:** So if the command is to create 5 pods then controller will take care of this but controller manager will handle and take care of the controller. It has 4 functions
- **Desired state:** Sees whats the desired state of the server being told by the API server for the controller
- **Current State:** Constantly checks if the operations meet the desired state
- **Differences & Make changes:** Listen to the changes & make the changes as being requested by api server

3) **Scheduler:** This is responsiple for physically scheduling the processes. It inspects the worker nodes and schedules the things accordingly.

4) **etcd:** It's the database that contains the infomation about the cluster so if the API server wants to get the information about the cluster the it will communicate with etcd.

### Worker node
1) **Kubelet:** Communicates with Container Runtime and with Control Plane API server. Whenever a new worker node is created and attached to the control plane, kubelet is installed on it.

2) **Kube-Proxy:** Communicates with Control Plane API server. Kube proxy is responsible for networking. This will allocate ip addresses to the worker node/ nodes

3) **Container Runtime:**
- **Pod:** It is the smallest scheduling unit. It monitors the health of the container, reinitiates one if one dies etc. This is similar to the controller manager (in the bigger picture). *Containers are inside a pod*
- **Container:** It's a simple container running your application or service inside it. Container is a isolated environment to build and run your application. You can read more if you like in my [Docker blog](https://kaiwalyakoparkar.hashnode.dev/docker-beginner-to-advance)
    

## Steps to run applications on Kubernetes

1) Create microservices

2) Containerize your microservices

3) Put container in pods

4) Deploy these pods to controllers

## K8s DNS
![](https://media.giphy.com/media/Zx1KzuQBR8wIbrm81t/giphy.gif)
This concept is pretty much understandable if you have worked with docker compose or other sorts of networking based communications between containers and services. If you haven't then don't worry. K8s DNS has some ip addresses for every pod and container so that they can communicate with each other, share information. From the previous application example you can imagine it as a way for your frontend containers to talk with your backend containers etc.a

## All required installations

1) [Docker Desktop](https://www.docker.com/products/docker-desktop/)

2) [Kubectl](https://kubernetes.io/docs/tasks/tools/)

3) [Minikube](https://minikube.sigs.k8s.io/docs/start/)


## Command Cheatsheets

### Minikube commands

```shell
$ minikube start

$ minikube status

$ minikube dashboard

$ minikube docker-env

# will switch to bash prompt of minikube
$ minikube ssh
```

### Kubectl commands

```shell
$ kubectl version --client

$ kubectl get pods

$ kubectl get nodes

# Shows information about the cluster
$ kubectl config view

# get everything like pods
$ kubectl get all

$ kubectl get deployments

$ kubectl create -f <pod-config yaml file>

# Get more info in wide format
$ kubectl get pod <pod-name> -o wide

# Get more info in yaml format
$ kubectl get pod <pod-name> -o yaml

# Port forwarding like docker
$ kubectl port-forward nginx-pod 8080:80

# Gets the replica sets
$ kubectl get rs view

# Get services
$ kubectl get services

# Apply the configurations to the k8s cluster
$ kubectl apply -f <file_name>.yml

# See the rollout history of the deployment
$ kubectl rollout history deploy/<name-of-deployment>

# Rollback to previous versions of the deployment
$ kubectl rollout undo deploy/<name-of-deployment> --to-revision <no-of-revision-from-history-command>
```

![](https://media.giphy.com/media/4zJa3fUd2yQA1jHARC/giphy.gif)

Well that's it, that is pretty much that goes around in kubernetes. You will understand and love it more once you build and deploy your application on it. Trust me best way to understand and learn kubernetes is through hands-on practice. Want to build an application and deploy it to your own cluster? Keep an eye on my blog page and there might be something for you in coming future 😉

## References
- [Kubernetes Tutorial for Beginners | What is Kubernetes? Architecture Simplified!](https://youtu.be/KVBON1lA9N8)
- [Kubernetes Course - Full Beginners Tutorial (Containerize Your Apps!)](https://youtu.be/d6WC5n9G_sM)
- [Kubernetes Tutorial for Beginners – Basic Concepts & Examples](https://spacelift.io/blog/kubernetes-tutorial)
