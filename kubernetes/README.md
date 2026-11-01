# Kubernetes Deployment

## Overview

Kubernetes was used to orchestrate the portfolio application locally using Minikube.

The application runs inside a Docker container using the image:

`maneesha0805/portfolio:v1`

## Environment

- Kubernetes
- Minikube
- kubectl
- Docker

## Deployment Configuration

The Kubernetes Deployment defines:

- Application name: portfolio
- Docker image: maneesha0805/portfolio:v1
- Number of replicas: 1
- Container port: 80

## Service Configuration

A NodePort Service exposes the portfolio application outside the Kubernetes cluster.

- Service name: portfolio-service
- Service type: NodePort
- Service port: 80
- Target port: 80
- NodePort: 31806

## Verification Commands

```bash
kubectl get deployments
kubectl get pods
kubectl get services
kubectl get nodes
```

## Deployment Commands

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

## Learning Outcomes

- Understanding Kubernetes Deployments and Pods.
- Running Docker images inside Kubernetes.
- Managing replicas.
- Exposing applications using NodePort Services.
- Verifying application availability using kubectl.
