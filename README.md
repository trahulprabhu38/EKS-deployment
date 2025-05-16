# AWS EKS Deployment Guide

This repository contains resources and instructions for deploying a Kubernetes cluster on AWS using Amazon EKS (Elastic Kubernetes Service) and deploying applications to it.

## Project Structure

- `deployment.yaml` - Sample 2048 game deployment configuration
- `ingress.yaml` - Ingress controller configuration for the 2048 game
- `namespace.yaml` - Kubernetes namespace definition for the game
- `steps/` - Documentation for each setup step
- `photos/` - Screenshots of the deployment process

## Getting Started

### Prerequisites

Before you begin, ensure you have installed the necessary tools as described in [prerequisites.md](steps/prerequisites.md):

- kubectl
- eksctl
- AWS CLI (configured with appropriate credentials)

### Installation Steps

Follow these steps in order:

1. [Installing EKS Cluster](steps/installing-eks.md)
2. [Configure OIDC Connector](steps/configure-oidc-connector.md)
3. [Install AWS Load Balancer Controller](steps/alb-controller-add-on.md)
4. [Deploy Sample Application](steps/sample-app.md)
5. [Deploy 2048 Game with Ingress](steps/2048-app-deploy-ingress.md)

## Deployment Files

This repository includes the following Kubernetes manifests:

- `namespace.yaml` - Creates a namespace called `game-2048`
- `deployment.yaml` - Deploys the 2048 game application with 5 replicas and creates a NodePort service
- `ingress.yaml` - Configures an ALB ingress to expose the 2048 game to the internet

## Deploying the 2048 Game

After setting up EKS and the AWS Load Balancer Controller, you can deploy the 2048 game using:

```bash
# Create the namespace
kubectl apply -f namespace.yaml

# Create the deployment and service
kubectl apply -f deployment.yaml

# Create the ingress
kubectl apply -f ingress.yaml
```

Alternatively, you can use the command provided in [2048-app-deploy-ingress.md](steps/2048-app-deploy-ingress.md):

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml
```

## Cleaning Up

To avoid incurring charges for resources you don't need, delete your EKS cluster when you're done:

```bash
eksctl delete cluster --name demo-cluster --region us-east-1
```

## Screenshots

The `photos/` directory contains screenshots of the deployment process for reference.# EKS-deployment
