# Minikube Scenario

Task: 
Prerequisites:
    - Create a Linux VM in your Azure Subscription
    - Connect with Remote SSH (VSCode Plugin) to your created Linux VM

    - Install the following components as well:
    - [Docker](https://docs.docker.com/engine/install/ubuntu/)
    - [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
    - [minikube](https://minikube.sigs.k8s.io/docs/start/)

Deployment in the minikube Kubernetes Cluster with following requirements:

    - minikube start (creates the single node cluster)
    - create a deployment which provides two containers
        - the following applications shoud be provided within the containers
            - container 1: busybox
            - container 2: minimal webserver deployment
    - use a service to expose the deployment
    - test the deployed service with kubectl port forward

This example is freely expandable.
Don't hesitate to ask questions!

Next step: refer to the expanded excercise