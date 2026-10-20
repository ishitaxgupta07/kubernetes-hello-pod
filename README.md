# Kubernetes Exercise 1: Hello Pod

A hands-on Kubernetes project that deploys an Nginx web server on a local Minikube cluster and exposes it through a NodePort Service.

## Business Scenario

Simulate a lightweight Zepto storefront web server using Nginx.

## Tech Stack

- Kubernetes
- Minikube
- Docker Desktop
- Nginx
- kubectl
- Git and GitHub

## Architecture

Browser -> NodePort Service -> Nginx Pod -> Minikube cluster

## Prerequisites

- Docker Desktop running
- Minikube
- kubectl

## Deployment

Start Minikube:

```powershell
minikube start --driver=docker
```

Deploy the Pod and Service:

```powershell
kubectl apply -f k8s/pod.yaml
kubectl apply -f k8s/service.yaml
```

Wait for the Pod to be ready:

```powershell
kubectl wait --for=condition=Ready pod/hello-k8s --timeout=180s
```

Verify resources:

```powershell
kubectl get nodes
kubectl get pods --show-labels
kubectl get services
kubectl get endpointslices -l kubernetes.io/service-name=hello-k8s
```

Open Nginx:

```powershell
minikube service hello-k8s
```

On Windows with the Docker driver, keep the terminal open while the service tunnel is active.

## Configuration

- Pod name: `hello-k8s`
- Container image: `nginx:stable`
- Container port: `80`
- Service type: `NodePort`
- NodePort: `30080`

## Cleanup

```powershell
kubectl delete -f k8s/service.yaml
kubectl delete -f k8s/pod.yaml
minikube stop
```

## Learning Outcomes

- Deploying containerized workloads using Kubernetes Pods
- Exposing applications through Services
- Writing declarative Kubernetes YAML manifests
- Understanding label selectors and service endpoints
- Verifying deployments and managing resources using kubectl
