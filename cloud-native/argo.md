# ArgoCD

Hey everyone in this blog we will see what is ArgoCD and in what ways it helps to overcome the drawbacks of the regular CI/CD pipeline while working with Kubernetes deployment

## What is ArgoCD?

ArgoCD is known as a declarative GitOps tool which is based on Kubernetes. Let's try to break this down. "GitOps" is a process where you take the code you have written and pushed to the Git registry (eg: GitHub, GitLab, Bitbucket) and take it to the deployment and this is mainly done and implemented as automation. The word "declarative" means that the deployment has exactly the same architecture that you want and have decided on. So if there was a case that something gets changed in the deployment then it will revert back to the previous state (the one which you have mentioned)

## CD workflow without ArgoCD:

So whenever the application is pushed to the git repository, there are certain steps it goes through to reach the deployment. These steps are automated and known as CI/CD pipeline. So once the code changes are pushed they are tested, the image is built, pushed to the DockerHub or other registry, Manifest files are updated and finally through kubectl apply... it is applied to the Kubernetes cluster.

But in this case, we have to face and resolve challenges like:

* Install and setup tools like kubectl
    
* Configuring access to Kubernetes
    
* Configuring access to could providers
    
* Several security challenges
    
* No visibility of deployment status
    

![Source: Tech with Nana youtube video](https://cdn.hashnode.com/res/hashnode/image/upload/v1676379180429/9d1ffd6a-e514-4caf-989b-1604a84d3a97.png)

## CD workflow with ArgoCD:

So in a general scenario the above-mentioned workflow is used, but while working with Kubernetes we might need to change this workflow. It is essential to know that according to the set best practice for the Git repository, we should have two separate repositories for Code files and application configuration (k8s manifests).

The main advantage is there can be a time we want to change only the config files but don't want the test -&gt; to build etc workflow to run as the configs can be changed independently of the application built. Having this as a reference now ArgoCD (which is installed on your Kubernetes Cluster) keeps track of the state you mentioned in the configuration repositories.

So if were to use the earlier CI/CD pipeline then it would have been too complex to manage and configure. Once the application is built and up the changes are reflected in the configuration files. These changes are detected by ArgoCD and pulled into the cluster.

> Note: ArgoCD works on the pull method and not like the usual push method

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676380750890/948970a3-9402-4a83-bc9c-cf44f121ee05.png)

## Advantages of using ArgoCD:

* **Git as a single source of truth:**
    
    This means that if any changes are to occur in the Kubernetes cluster then the git repository is a place to validate and check if everything is going as mentioned in the manifests and any instance that is out of instructions is rolled back.
    
* **Easy rollback:**
    
    This is a very essential feature of ArgoCD as it helps us to revert to the previous state if there was any problem or misconfiguration in the cluster.
    
* **Cluster disaster recovery:**
    
    This means if one of my servers were to go down then I can create another cluster with ArgoCD and point it to the same repository then the process for recovery becomes much more efficient and fast
    
* **K8s access control:**
    
    We can manage the cluster access directly through git so we don't have to worry about giving access to the cluster to an external tool.
    

### Let's try it out!

ArgoCD is super easy to install and configure. We will be looking at it through an example. I will be using Minikube for my Kubernetes Cluster.

I will be using this repository for [this](https://github.com/kaiwalyakoparkar/practical-devops/tree/main/ArgoCD) demo purpose and you can use the same

1. Install ArgoCD into your cluster using the following commands
    

```bash
kubectl create namespace argocd
```

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

1. Now that we have installed the argocd in the argocd namespace we can now create a yaml file with the following code. I will name the YAML file as `application.yaml`.
    

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: wmd-argo-application
  namespace: argocd
spec:
  project: default

  source:
    #Your repo link here
    repoURL: https://github.com/kaiwalyakoparkar/practical-devops.git
    targetRevision: HEAD
    #Location where the manifests are stored
    path: ArgoCD/dev
  destination: 
    server: https://kubernetes.default.svc
    namespace: wmd

  syncPolicy:
    syncOptions:
    - CreateNamespace=true

    automated:
      selfHeal: true
      prune: true
```

1. Create a `dev` folder and place your deployment and service files into it like below. (Notice that it's the same path which I have mentioned in above `application.yaml` file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676384489504/0e9b4cd0-30de-4f31-a2c8-12d7203e55f1.png)

1. Let's create a namespace for our application as we have mentioned in the manifest files. (Again the manifest files like `deployment.yaml` and `service.yaml` are already present on the repo so you can check them out there
    

```bash
# You can give any name to your namespace and update respective files
kubectl create namespace wmd
```

1. Now we have to apply the `application.yaml` file to the cluster. We can do that using the `kubectl apply` command like below
    

```bash
kubectl apply -f application.yaml
```

1. Let's go and check out it on the ArgoCD dashboard. To see the dashboard run the following command on your terminal
    

```bash
kubectl port-forward svc/argocd-server 8080:443 -n argocd
```

and now you can go to `http://localhost:8080` to access the ArgoCD dashboard

1. In the `Username` field enter `admin` and to generate a password run the following commands into the terminal
    

```bash
 kubectl get secret argocd-initial-admin-secret -n argocd -o yaml
```

and you will get output something like:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676385052217/39ea7218-3c12-4e8a-ae27-7e1ba2151107.png)

We are not done yet, copy the password in this case mine will be `VktPYkNUZGZRcjlNVk1ibQ==` now put this password into another command to decode it and obtain the real password. Run the following command to decode it

```bash
# Change after echo with your password
echo VktPYkNUZGZRcjlNVk1ibQ== | base64 --decode
```

Now copy the password that is obtained (Remember to omit `%` at the end of the password obtained) and put it into the ArgoCD dashboard

1. Now you will be able to view the application in the dashboard
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676385309478/b06800fa-7e3a-4450-a3d2-fa5d7d3fe633.png)

Click on the application name and you are able to see a beautiful map of your deployment

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676385374374/a388639a-8fbd-457a-876d-5c2cc555a866.png)

You can see every possible information about the cluster here including the health of the pod, cluster and service. ArgoCD pulls the changes every 3 minutes this can be changed using webhooks and other methods.

### Resources:

* [ArgoCD documentation](https://argo-cd.readthedocs.io/en/stable/)
    
* [ArgoCD Tutorial for Beginners | GitOps CD for Kubernetes](https://youtu.be/MeU5_k9ssrs)
    
* [What is ArgoCD](https://youtu.be/p-kAqxuJNik)