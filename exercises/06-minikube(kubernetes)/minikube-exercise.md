# Documentation (en) minikube

## Introduction

1 Summary:

To get a small overview over the topic and create some groundwork we need to get to know some of the terms. 

First, do some research on these terms to get an understanding of the concepts you will be working with.  

2 The environment:

The environment of this task is [minikube](https://minikube.sigs.k8s.io/docs/), which is a local version of [Kubernetes](https://kubernetes.io/), focussing on making it easy to learn and develop for Kubernetes.

Kubernetes is a container orchestration system for automating the deployment, scaling, and management of containerized applications. It allows for easy management and discovery.

3 Goal:

Creating a deployment with two containers, one web service container and one busybox container,  accessible from the Internet via a service and an ingress.

## Get started

To get started you need to fulfill these Prerequisites: 

[installing docker on ubuntu](https://docs.docker.com/engine/install/ubuntu/) 

[install-kubectl-linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

[minikube start](https://minikube.sigs.k8s.io/docs/start/)

You will need [kubectl](https://kubernetes.io/docs/reference/kubectl/):

- Kubectl is a command line tool you will need to navigate and manage your Kubernetes Cluster, deploy applications in your cluster etc.

### Prerequisites - connecting a Linux VM to VSCode on a Windows machine

To connect a Linux virtual machine (VM) to Visual Studio on a Windows machine, follow these steps:

1. Create a Linux VM in Azure: 
    1. Go to the Azure portal and sign in with your account
    2. Click on the "+ Create a resource" button and search for "Linux VM"Select the "Ubuntu Server 20.04 LTS" image and click on "Create"
    3. Follow the prompts to configure the VM settings, including the VM name, size, user name and password, and network settings
    4. Click on "Create" to create the VM
2. Download and install the "Remote - SSH" extension in Visual Studio Code:
    1. Open Visual Studio Code and click on the "Extensions" icon on the left side of the window
    2. Search for "Remote - SSH" and click on "Install" for the extension by Microsoft
    3. Restart Visual Studio Code to complete the installation
3. Configure the connection to the Linux VM in Visual Studio Code:
    1. Click on the "Remote Explorer" icon on the left side of the window
    2. Click on the gear icon and select "Create a new SSH host"
    3. In the "Host" field, enter the name of the Linux VM (e.g. "LinuxVm")
    4. In the "HostName" field, enter the public IP address of the Linux VM (e.g. "20.16.205.159")
    5. In the "User" field, enter the user name of the Linux VM (e.g. "azureuser")
    6. In the "IdentityFile" field, enter the path to the .pem file that you downloaded when creating the Linux VM (e.g. "Path_to_your_config\id_rsa") 
    7. Click on "Save" to save the configuration
4. Connect to the Linux VM from Visual Studio Code:
    1. Click on the "Remote Explorer" icon on the left side of the window
    2. Under the "SSH Targets" list, select the Linux VM (e.g. "LinuxVm")
    3. Click on the "Connect" button to connect to the Linux VM

To install and use the kubectl command-line tool on the Linux VM, follow these steps:

1. [Install the kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) tool on the Linux VM
2. You can now use the kubectl tool to manage Kubernetes clusters. For example, to list the nodes in a cluster, run the following command: 
kubectl get nodes (this only works after you started a minikube cluster)

## Task summary

1. minikube start (creates the single node cluster)
2. create a deployment which provides two containers
    1. the following applications shoud be provided within the containers
        - container 1: busybox
        - container 2: minimal webserver deployment
3. use a service to expose the deployment
4. test the deployed service with kubectl port forward

### 1 Create the cluster and connect to it

- What is a [cluster](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/)?
    - A set of Nodes that run containerized applications managed by Kubernetes. For this example, and in most common Kubernetes deployments, nodes in the cluster are not part of the public internet.
- connect to it in the command line

### 2 Create a deployment with two containers

- What is a [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) in Kubernetes?
    - A deployment is a way to manage and run multiple [replicas](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) of an application. It helps keep the desired number of copies running at all times, and can automatically replace any copies that stop working. Deployments can also be used to update the application by creating new copies with updated code or settings, and then gradually replacing the old copies with the new ones.
- What is a [Container](https://kubernetes.io/docs/concepts/containers/)?
    - In Kubernetes, a container is a process that runs within a [Pod](https://kubernetes.io/docs/concepts/workloads/pods/). It is defined using a configuration file. The file specifies the container image to use, any options or environment variables that should be passed to the container, and any resources that the container should be allocated (e.g. CPU and memory).
    - Containers are isolated from each other and bundle their own libraries and dependencies, allowing applications to run smoothly and consistently, regardless of the host environment.
- create a [yaml](https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started) file as a configuration file and define your deployment and the containers:
    - [busybox](https://busybox.net/about.html)
    - webserver

### 3 Use a Service to expose the Deployment

- What is a [Service](https://kubernetes.io/docs/concepts/services-networking/service/) in Kubernetes?
    - In Kubernetes, a Service is an abstract way to expose an application running on a set of Pods as a network service. When you create a Service, it creates a virtual IP (VIP) that routes traffic to the appropriate Pods. This way, you don't have to worry about the underlying network infrastructure or the details of the Pods. You can just specify the desired state of your application, and Kubernetes takes care of the rest.
    - There are several types of Services in Kubernetes, including ClusterIP, NodePort, and LoadBalancer. A NodePort Service exposes the service on a specific port on each node in the cluster, allowing external traffic to access the service.
- Create a Service that exposes your Deployment

### 4 Port Forward

- What is [Port forwarding](https://www.weave.works/blog/kubectl-port-forward#:~:text=Kubectl%20port%2Dforward%20is%20a,commands%20and%20control%20Kubernetes%20clusters.)?
    - Kubectl Port forwarding is used to access your Kubernetes Cluster from your local machine.
    - Port forwarding redirects a communication request from one network node to another. It is often used to allow remote access to a device or service on a private network from a device or service on a public network, such as the Internet.
- e.g: **kubectl port forward --address 0.0.0.0 -n namespace svc/svc-name 8080:80**
- First, make your cluster reachable via the internet by starting minikube in docker with the public ip of the VM: **minikube start --vm-driver=docker --apiserver-ips=0.0.0.0** (the public ip of your VM)
- Now use port forwarding to connect to a service via your local browser (use the public ip)

That's it! You should now have a deployment with two containers accessible from the Internet via a service and an ingress.

 [command line based example](https://kubernetes.io/docs/tutorials/hello-minikube/)
