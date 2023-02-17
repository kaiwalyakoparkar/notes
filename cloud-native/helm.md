# Helm

## What is Helm?

Helm is a tool that helps in defining, upgrading, and managing the deployments that are needed in your Kubernetes cluster. Helm also works as a template engine which makes it really helmful (intended pun - helpful 😅) when you are working across teams with lots of files and configurations. Let's see some feature understanding everything I just mentioned in detail.

## Features of Helm

### 1\. Package Manager and Charts:

Helm is used to package yaml files. These yaml files are deployment and config files for the application you want in your Kubernetes Cluster. This makes it easier to distribute these files as packages in public for private repositories.

For example, if you want to use Elastic Stack. For including it in your cluster you will have to write the `deployment` yaml files, create `secrets`, `configmaps`, `Kubernetes user with Permissions`, and multiple `Services`. And anyone who wants to use the Elastic stack will have to repeat this process again. What if someone packaged everything ready into a template format so that it becomes more manageable for everyone? That is indeed done. These packages and called Helm Charts. These charts can be shared via repositories.

![](https://i.imgur.com/FX4WBz8.png align="center")

### 2\. Templating Engine

Let's say you have an application with multiple microservices running. The config yaml files for these microservices are identical and the only thing changes is `name`, `image` name etc. In the ideal case, you will create separate files with exact same code for every microservices. Helm helps you create templates of these exact same code converting it into just one file and all the variable properties go under the values file. Let's see how these files look like

```yaml
#Template for pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: {{ .Values.name }}
spec:
  containers:
  - name: {{ .Values.container.name }}
    image: {{ .Values.container.image }}
    port: {{ .Values.container.port }}
```

```yaml
#values.yml
name: my-app
container:
    name: my-app-container
    image: my-app-image
    port: 9001
```

Following is the logical diagram for the working of template and config files

![Argo CD Working With Helm | Kube by Example](https://raw.githubusercontent.com/christianh814/kbe-guide/main/04-argocd-working-with-helm/img/helm.jpg align="center")

### 3\. Release Management

One of the other prominent feature of helm is release management. Helm version comes in 2 parts `helm cli` and `helm server` (also called as `Tiller`). So the cli sends the request to the server (which runs inside the kubernetes cluster) and upon request `Tiller` creates the components like `pods` and `services` inside Kubernetes cluster. This offers the release management feature.

When you create a deployment `Tiller` keeps a copy with itself for future references creating a release history and when you run something like `help upgrade <chartname>` for upgrading version for example`version: 1.14.2` then the current deployments are updated instead of removing the deployments and starting new once. This helps in seamless roll-in and roll-out feature

![Simplifying App Deployment in Kubernetes with Helm Charts | by Kirill  Goltsman | Supergiant.io | Medium](https://miro.medium.com/max/646/1*1lHh6xk05cs9AO3w-vh7iA.jpeg align="center")

## Downside of Helm:

### Security issue caused by Tiller:

Although `Tiller` has amazing use cases but it has too many permissions to your Kubernetes Cluster like `CREATE`, `UPDATE`, `DELETE` and hence raises a big security threat. Thus in the Helm version 3, the `Tiller` has been removed and is now just helm binary.

So this takes the release management feature from Helm and makes it bit more difficult.

### Helm Commands - Cheatsheet

You can use this cheatsheet for popularly used Helm commands

```bash
#Helm chart creation
helm create <name>

#Helm install
helm install <name> <repo-name>

#Listing version
helm list <flag>

#Pulling helm charts
helm pull <chart URL | repo/chartname>

#Pushing helm chart
heml push <name> <repo-name>

# add a chart repository
helm repo add <chart-name> 

#generate an index file given a directory containing packaged charts
helm repo index <chart-name> 

# list chart repositories
helm repo list <chart-name> 

# remove one or more chart repositories
helm repo remove <chart-name> 

# update information of available charts locally from chart repositories
helm repo update <chart-name> 

# search a keywork in chart
helm search repo <keyword>
```

## References 📖

* [Helm Documentation](https://helm.sh/docs/)
    
* [What is Helm?](https://youtu.be/fy8SHvNZGeE)
    
* [What is Helm in Kubernetes? Helm and Helm charts explained](https://youtu.be/-ykwb1d0DXU)
    
* [kaiwalyakoparkar/practical-devops](https://github.com/kaiwalyakoparkar/practical-devops)
    
