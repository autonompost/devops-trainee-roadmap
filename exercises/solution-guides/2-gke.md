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

4. The Deployment should be reachable via the Internet
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