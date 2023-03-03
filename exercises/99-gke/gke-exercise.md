# Documentation (en) GKE 

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
Install gcloud CLI(https://cloud.google.com/sdk/docs/install#deb)
1. Install the kubectl tool on the Linux VM:
    1. Open a terminal window on the Linux VM and enter the following command: 
    sudo apt-get install kubectl
3. You can now use the kubectl tool to manage Kubernetes clusters. For example, to list the nodes in a cluster, run the following command: 
kubectl get nodes

## Task

1. create a Cluster and connect to it 
2. create a deployment which provides two containers
    1. the following applications shoud be provided within the containers
        - container 1: busybox
        - container 2: minimal webserver deployment (connect this container with the ingress)
3. use a service to expose the deployment
4. the deployment should be reachable via the internet → ingress (also look at ingress annotations)

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

### 4 Ingress

- What is [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)?
    - An Ingress is a collection of rules that allow inbound connections to reach the cluster services. It defines how external traffic should be routed to a service within the cluster. It is defined using YAML files, and consists of a set of rules that specify the connection properties and behavior of the Ingress.
    
    Ingress resources can also be used for load balancing, SSL termination, and name-based virtual hosting. They can also be used to route traffic to multiple services based on the request hostname or path, or to perform content-based routing.
- [Ingress Controller](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)
    - An  Ingress Controller is needed in the cluster for the Ingress resource to work. It accepts incoming HTTP/HTTPS traffic and is responsible for routing it to the correct service.
    - It is usually deployed alongside the services that it is routing traffic to. It listens for incoming traffic and processes it according to the rules defined in ingress resources, which specify how traffic should be routed to the services.
- Create an Ingress Controller configuration and deploy it
- Configure an Ingress resource that exposes the Service you created in the previous step

That's it! You should now have a deployment with two containers accessible from the Internet via a service and an ingress.

 [command line based example](https://kubernetes.io/docs/tutorials/hello-minikube/)

### Guide:

- 1 Create a cluster and connect to it
    1. start minikube on your Linux VM with the command: **minikube start**. This will create a Kubernetes-Cluster within the VM.
    2. run the command **kubectl config use-context minikube** to connect to the cluster
- 2 Create a Deployment, which will provide two containers
    1. Create a file named deployment.yml that contains the definition for the deployment. The deployment should contain two containers, a busybox container and a web server container. A definition of the deployment might look like this: 
        
        ```yaml
        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: nginx
          namespace: web-svc
          labels:
            app: nginx
        spec:
          replicas: 1
          selector:
            matchLabels:
              app: nginx
          template:
            metadata:
              labels:
                app: nginx
            spec:
              containers:
              - name: nginx
                image: nginx
                ports:
                - containerPort: 80
              - name: busybox 
                image: busybox
                command:
                  - sleep
                  - "3600"
                ports: 
                - containerPort: 80
                imagePullPolicy: IfNotPresent
        ```
        
    2. create this definiton with the command **kubectl apply -f pod.yml**.
    - the following applications should now to be deployed in the pods:
        1. the busybox application has already been specified as one of the containers in the deployment definition.
        2. the web server was also specified in the deployment definition as one of the containers.
- 3 Use a Service to expose the Deployment
    1. Create a file named service.yml that contains the definition for the service. The service should expose the deployment you created in the previous step. A definition of the service might look like the following:
        
        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          name: nginx-service
          namespace: web-svc
        spec:
          selector:
            app: nginx
          type: NodePort
          ports:
          - protocol: TCP
            port: 80
            targetPort: 80
        ```
        
    2. Create the service with the command **kubectl apply -f service.yml**.
- 4 The Deployment should be reachable via the Internet
    1. Create an Ingress Controller (once), the definition for the Ingress Controller might look like this:
        
        ```yaml
        apiVersion: v1
        kind: Service
        metadata:
          namespace: ingress-nginx
          name: task-svc-1
        spec:
          selector:
            app.kubernetes.io/name: ingress-nginx-controller
          ports:
          - name: http
            protocol: TCP
            port: 80
            targetPort: 80
        ```
        
    2. Create a file named ingress.yml that contains the definition for the ingress. The ingress should expose the service you created in the previous step. A sample definition of the ingress might look like this:
        
        ```yaml
        apiVersion: networking.k8s.io/v1
        kind: Ingress
        metadata:
          name: minimal-ingress-1
        spec:
          ingressClassName: nginx
          rules:
          - http:
              paths:
              - path: /
                pathType: Prefix
                backend:
                  service:
                    name: task-svc-1
                    port:
                      number: 80
        ```
        
    3. Create the Ingress with the command **kubectl apply -f ingress.yml**.