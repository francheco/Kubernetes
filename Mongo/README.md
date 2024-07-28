
### Provisioning

# Install Minikube

brew install minikube

# Install kubectl

brew install kubectl

# Start Minikube Cluster with Docker Driver

minikube start --nodes 2 --driver=docker

--nodes 2: Specifies the number of nodes to create in the cluster.

# Create Namespace

kubectl create namespace mongo

kubectl get namespaces

Namespaces are used to organize Kubernetes resources in a cluster. They allow multiple teams to work in the same cluster without conflict

# Create MongoDB Secret

Before creating the MongoDB deployment, first create the Secret to store the MongoDB username and password

encode the values

echo -n "mongodb" | base64

echo -n "admin" | base64

then create the mongo-secret.yaml file

Create the Secret

kubectl apply -f mongo-secret.yaml

kubectl get secrets -n mongo

kubectl describe secret mongo-secret -n mongo



# Create Mongo Express Secret

create the Secret to store the Mongo Express username and password

encode the values

echo -n "express" | base64

echo -n "admin" | base64

then create mongo-express-secret.yaml

Create the Secret

kubectl apply -f mongo-express-secret.yaml

kubectl get secrets -n mongo

kubectl describe secret mongo-express-secret -n mongo



# Create ConfigMap for Mongo Express

ConfigMaps help store non-sensitive configuration data that the application can use

Create a file named mongo-express-configmap.yaml

Then deploy it

kubectl apply -f mongo-express-configmap.yaml

kubectl get configmaps -n mongo

kubectl describe configmap mongo-express-config -n mongo




# Create the MongoDB Deployment

Create a file named mongo-deployment.yaml

Then, Deploy it

kubectl apply -f mongo-deployment.yaml

kubectl get deployments -n mongo

kubectl get pods -n mongo


# Create the Mongo Express Deployment

Create a file named mongo-express-deployment.yaml

Then, Deploy it

kubectl apply -f mongo-express-deployment.yaml

kubectl get deployments -n mongo

kubectl get pods -n mongo



# Create MongoDB Service

Kubernetes services provide stable endpoints for Pods, allowing them to communicate with each other and outside clients.

Create a file named mongo-service.yaml

Then, Deploy it

kubectl apply -f mongo-service.yaml

kubectl get services -n mongo

A ClusterIP service exposes the service only within the cluster


# Create Mongo Express Service

Create a file named mongo-express-service.yaml

Then, Deploy it

kubectl apply -f mongo-express-service.yaml

kubectl get services -n mongo

A LoadBalancer service It allows external users to access the service from outside the cluster.


# Global validations

kubectl get pods -n mongo

kubectl get services -n mongo

minikube service mongo-express -n mongo

This command will open the Mongo Express service in your default web browser.

If you prefer to access it manually, obtain the Minikube IP and combine it with the NodePort

minikube IP

Then access Mongo Express using

http://<MINIKUBE_IP>:30000

This setup guide should address all the requirements for deploying a fully functional MongoDB and Mongo Express application using Kubernetes on your local machine with Minikube.


