# My ecosistem DevOps
This repository create containers to different tools with durable data.

## 1. Steps to start Docker Compose

```sh
./start.sh
docker-compose up --build
Jenkins   -> http://localhost:8080/
Nexus     -> http://localhost:8081/
Sonarqube -> http://localhost:8082/
```

## 2. Steps to start Kubernetes

### Create minikube cluster
```sh
minikube start 
kubectl get nodes
minikube status   
kubectl version
```
###  Create Namespace "devops"
```sh
kubectl create -n devops
```
###  Create volumens in host "minikube"
```sh
minikube ssh
mkdir /home/docker/volumen-jenkins
```

###  Run service
```sh
kubectl apply -f jenkins-deployment.yaml
kubectl apply -f jenkins-service.yaml
```
###  Run dashboard
```sh
kubectl proxy
kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"
```
You can see the dashboard [here](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/) and use the previous token.