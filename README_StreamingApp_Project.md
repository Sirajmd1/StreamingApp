# StreamingApp DevOps Project

## Project Overview

This project demonstrates end-to-end DevOps implementation for a MERN-based Streaming Application using Docker, Amazon ECR, Jenkins, Amazon EKS, Helm, CloudWatch, and GitHub.

**GitHub Repository**: https://github.com/Sirajmd1/StreamingApp

## Architecture

GitHub -> Jenkins Pipeline -> Docker Build -> Amazon ECR -> Amazon EKS -> Helm Deployment -> CloudWatch Monitoring -> SNS Notifications

## Technologies Used

- Git & GitHub
- Docker
- Jenkins
- Amazon ECR
- Amazon EKS
- Helm
- Kubernetes
- AWS CLI
- Amazon CloudWatch
- Amazon SNS
- Node.js / MERN Stack

## ECR Repositories

- streaming-frontend
- admin-service
- auth-service
- chat-service
- streaming-service

AWS Account ID: 258274811560

## Project Workflow

### 1. Version Control
- Forked repository from upstream.
- Synced upstream changes when required.
- Maintained source code in GitHub.

### 2. Containerization
- Created Dockerfiles for frontend and backend services.
- Built Docker images.
- Tested local container execution.

### 3. Amazon ECR
- Created ECR repositories.
- Authenticated Docker with ECR.
- Tagged and pushed application images.

### 4. Jenkins CI/CD
- Installed Jenkins on EC2.
- Configured Git integration.
- Created pipeline for:
  - Checkout
  - Build
  - ECR Login
  - Docker Image Push

### 5. Kubernetes Deployment
- Created EKS cluster.
- Configured kubectl and eksctl.
- Deployed workloads using Helm.

### 6. Helm Configuration
Services included:

- streaming-frontend
- admin-service
- auth-service
- chat-service
- streaming-service

Frontend deployed using LoadBalancer service.
Backend services deployed using ClusterIP.

### 7. Monitoring and Logging
- CloudWatch Metrics
- CloudWatch Logs
- Kubernetes Pod Monitoring
- EKS Health Monitoring

### 8. ChatOps
- SNS Topic creation
- Email/Chat notifications for deployment events

## Jenkins Pipeline Stages

1. Checkout Source
2. ECR Login
3. Build Frontend Image
4. Build Admin Service Image
5. Build Auth Service Image
6. Build Chat Service Image
7. Build Streaming Service Image
8. Tag Images
9. Push Images to ECR

## Deployment Commands

### Helm Install

```bash
helm install streaming-app ./streaming-app
```

### Helm Upgrade

```bash
helm upgrade streaming-app ./streaming-app
```

### Verify Deployment

```bash
kubectl get pods
kubectl get svc
kubectl get deployments
```

## Validation Checklist

- [x] GitHub Repository Created
- [x] Dockerfiles Created
- [x] Jenkins Pipeline Configured
- [x] ECR Repositories Created
- [x] EKS Cluster Configured
- [x] Helm Deployment Completed
- [x] Monitoring Configured
- [x] Documentation Created

## Repository Structure

```text
StreamingApp/
├── frontend/
├── backend/
│   ├── adminService/
│   ├── authService/
│   ├── chatService/
│   └── streamingService/
├── Jenkinsfile
├── Chart.yaml
├── values.yaml
├── templates/
└── README.md
```

## Author

Sirajuddin Mohammed
IT Engineer, Staff
Hyderabad, India
