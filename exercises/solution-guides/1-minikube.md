### Guide:

1. Create a cluster and connect to it
  1. start minikube on your Linux VM with the command: **minikube start**. This will create a Kubernetes-Cluster within the VM.
  2. run the command **kubectl config use-context minikube** to connect to the cluster
2. Create a Deployment, which will provide two containers
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

3. Use a Service to expose the Deployment
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

4. Port Forwarding
  1. starting minikube in Docker 
  1. starting minikube in Docker: **minikube start --vm-driver=docker --apiserver-ips=0.0.0.0** (public ip of vm)
  2. Port forward the desired service: **kubectl port forward --address 0.0.0.0 -n namespace svc/svc-name 8080:80** (0.0.0.0 makes is publicly available)
  3. go to local machine and go to browser and type the VM’s public ip address
