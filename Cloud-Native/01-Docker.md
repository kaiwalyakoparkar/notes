# Docker

## What is Docker?

Docker is a tool which helps you run you application in isolated environment. Docker creates a isolated environment often called "container" where you run your application without getting affected by external factors. This helps in solving the major problem and often a joke "But this works on my computer". You can easily share images to spin up containers and it would work exactly the same as it would run on the machine it was built on. This is very effective tool while deploying your application to production

![What is docker](https://i.imgur.com/yIvuoYU.png align="left")

## Steps to Containerize your application

In this section we will see 3 essential steps you need to follow in order to containerize your application

![steps of cont](https://i.imgur.com/nXkKoQ7.png align="left")

### Dockerfile

This file is often referred as "recipe" for your container. This is a simple file which contains all and each step to setup and run your project. This file needs every detail from packages you install to the command you run in order to run that specific application. We will look more into how you can build your own dockerfile in the coming sections

### Docker Image

Image is what you build out of your dockerfile. Image is easily sharable and storable. So if you want someone to try out your application you can just send them this docker image and they would be able to run the application exact same way without setting up anything on their local machines. Or even you can use these images to push your application in the production. You can think this a "class" from the "object oriented programming" reference.

### Docker Container

Container is the running instance of an application. Containers are the built and setup using docker images. So whenever you get an image and you run it then a 'container' is created with all the information and this is the step where your application is actually running. You can create multiple containers from single image. You can think this as "object" from the "object oriented programming" reference.

![Run multiple containers](https://i.imgur.com/Ro2YJ44.png align="left")

## Build your first Dockerfile

Every step in the docker file acts as a layer for next step while building the image out of it. Let's take a simple docker file as an example.

```bash
FROM node:alpine
COPY . ./
RUN npm install
CMD ["npm", "start"]
```

This is a dockerfile for a simple nodejs api script.

* `FROM` : This specifies the base os image on which your application needs to run. This is one of the essential fields you need to mention in your dockerfile
    
* `COPY`: This is simple copy command which has 2 preceding arguments. 1 - the files you need to copy, in this case all so `.` and where you need to copy so in this case `./` root directory
    
* `RUN`: You add a command here which you want to execute during the building of the container. In this case I did `npm install` because well I need `node_modules` folder to run my nodejs application
    
* `CMD`: This is where you add the command you need to run after the container is created and set up. You can keep on adding the commands in this array. If it's only one command then you don't necessarily need to put it in the array format.
    

## Basic Docker Commands

### Status Checking Commands

```bash
#Check docker version
$ docker -v

#See all the images in docker
$ docker image ls #[OR]
$ docker images

#See the runnig containers
$ docker container ls

#See all the containers
$ docker container ls -a

#See the running docker processes
$ docker ps

#See all the docker processes
$ docker ps -a

#Inspect a docker container
$ docker inspect <container-name>/<container-id>

#Inspect a docker image
$ docker inspect <image-name>/<image-id>

#See all the networks on host
$ docker network ls
```

### Execution Commands

```bash
# Pull an image from dockerhub
$ docker pull <image-name>

# Run the image (if not present on device then it will pull and run)
$ docker run <image-name>

# Run the image with specific version
$ docker run <image-name>:<version>

# Run the image with attached linux command (Command comes after image name)
$ docker run <image-name> echo hello

# Run the image in interactive mode
$ docker run -it <image-name>

# Run the image in detached mode (in background)
$ docker run -d <image-name>

# Run the appliation running in the container into your machine with port forwarding
$ docker run -d -p <local-port(eg: 8080)>:<service-default-port> <image-name>
eg:
# You can now acces ngix on https://localhost:8080
$ docker run -d -p 8080:80 nginx

# Start Container
$ docker start <container-name>/<container-id>

# Stop Container
$ docker stop <container0name>/<container-id>

# Remove image
$ docker rmi <image-name>/<image-id> -f

# Remove container
$ docker rm <container-name>/<container-id>

# Get the logs of the running container
$ docker logs <container-id>
```

## Building and Deploying Commands

```bash
# Build your on docker file
$ docker build -t <image-name>:<image-version> <dockerfile-path>

# Push the image to docker hub
$ docker push <hub-user>/<repo-name>:<tag>
```

## Networking in Docker

When you install docker it create 3 networks automatically

### Bridge:

* It is the default network that gets attached with the container.
    
* It is a private and internal network created by docker on host.
    
* Every container gets a internal ip address and containers can access each other using this internal ip address.
    
* To access any container from external you need to map the port of the container to ports of docker host
    
* You can run multiple web containers on same docker host and on the same port
    

![Default Docker Network](https://i.imgur.com/FRd7AuM.png align="left")

### None:

* In this type the container is not connected to any network.
    
* This means it has no connections with external networks nor other containers on the same docker host.
    
* And the container will run in totally isolated network.
    
* Use the following command to attach this network to your container
    

```bash
$ docker run <image-name> --network=none
```

![None network](https://i.imgur.com/0qMamCQ.png align="left")

### Host:

* To access the container externally you can attach the host network parameter to the container and it takes out any network isolation between docker host and docker container.
    
* So if you have web app container with port 5000 then it can be accessed at same port expertally without the port mapping.
    
* Now this means you can't have multiple containers running on the same docker host and on the same port as port are now common to all the containers on the host network
    
* Use the following command to attach this network to your container
    

```bash
$ docker run <image-name> --network=host
```

**eg of the host:** Taking same example as `nginx` from above

```bash
# with port mapping http://localhost:80
$ docker run -d -p 80:80 nginx

# without port mapping, host networking http://localhost:80
$ docker run -d nginx --network=host
```

![Host Network](https://i.imgur.com/008w9jq.png align="left")

### User-define networks

When we create containers on same docker host there is only 1 bridge created connecting all the containers by default. (eg: 172.17.0.1) and you want to create a new bridge maybe with ip (182.18.0.1) on the same host you need to do it through thte command

```bash
$ docker network create \
    --driver bridge \
    --subnet 182.18.0.0/16
    custom-isolate-network
```

![User Defined Network](https://i.imgur.com/yPy1BFx.png align="left")

## Docker Compose

Docker compose is a feature provide by docker host to connect and spin up multiple containers with mostly different images but the application is dependent on both the images quickly.

![](https://i.imgur.com/P1LSF4m.png align="left")

For example frontend image eg: `voting` and backend database in `mongodb` so let's try creating a docker compose file for it

```yml
version: 2
services:
    voting:
        image: local-fe-voting
        network: 
             - frontend
    db:
        image: mongo
        network: 
            - backend
        
#This will create different networks on same docker host
networks:
    frontend:
    backend:
```

## Docker Engine/ Architecture

Let's see the docker architecture and how it runs applications in containers under the hood. When you install docker on your computer you essentially downloading 3 different components

![Architecture](https://i.imgur.com/xOSb5JO.png align="left")

### Docker Deamon

It is a backgroud process that manages docker objects like images, containers, volumes etc

### REST API

It is a programming interface used to talk to the docker deamon and provide instructions. You can use this api to create your own differnt docker tools

### Docker CLI

And this is a CLI that we have used until now to perform action. It uses REST API to talk to the docker deamon. Now the thing to note here is docker cli need not to be on same host. It can be on different computer and can still communicate with remote docker engine. Use the following command to do so

```bash
$ docker -H=<remote-docker-engine>:<port-number>

#example with nginx remote docker engine
$ docker -H=10.123.2.1:2375 run nginx
```

## Container Orchestration

With simple `docker run` command you create instance of your application but that's just one instance what if you wanted to create multiple instance. In that case you will have to run `docker run` command multiple time. Not just this you will have to closly monitor the health of each container and spin up new instance if one already running likely goes down. And what about the health of docker host? What if the docker host goes down, in that case the containers hosted on that host becomes inaccessble too. Orchestration is set of tools and scripts that helps us to host the containers in the real production environment. Generally Container Orchestration solution have multiple docker hosts that can host containers. So even if one fails, application is still accessible to others. The following is the command used in docker swarm

```bash
$ docker service create --replicas=100 nodejs
```

![Container Orchestration](https://i.imgur.com/T6yy5f6.png align="left")

There are multiple orchestrations solutions available now a days

* Docker Swarm
    
* Kubernetes
    
* Mesos
    

Well we deep dived quite a bit into the details of docker from simple commands to architecture but that's it for this blog. See you in the next one :D

### References:

* [Docker Tutorial for Beginners - What is Docker? Introduction to Containers](https://youtu.be/17Bl31rlnRM)
    
* [Docker Tutorial for Beginners - A Full DevOps Course on How to Run Applications in Containers](https://youtu.be/fqMOX6JJhGo)