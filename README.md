# Kriyadocs DevOps Case Study

This repo simulates a full DevOps pipeline using Ansible, Jenkins, Docker, Helm, and Kubernetes.

## Stack Simulated

- AWS VPC & EC2 provisioning via Ansible (simulated)
- Jenkins CI/CD
- Node.js, Python (Flask), PHP apps
- Deployed via Helm to local Minikube K8s cluster
- Docker-based builds
- Rancher-ready (optional)

## How to Run

### 1. Setup

Install Docker, Minikube, Helm, Jenkins, Ansible using Homebrew.

Start:
```bash
minikube start --driver=docker
brew services start jenkins-lts

2. Simulate Provisioning

ansible-playbook ansible/provision.yml --check

