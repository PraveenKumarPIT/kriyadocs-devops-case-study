# Kriyadocs DevOps Case Study

This repo simulates a full DevOps pipeline using Ansible, Jenkins, Docker, Helm, and Kubernetes.

## Stack Simulated

- AWS VPC & EC2 provisioning via Ansible (simulated)
- Jenkins CI/CD
- Node.js, Python (Flask), PHP apps
- Deployed via Helm to local Minikube K8s cluster
- Docker-based builds
- Rancher-ready (optional)

## Overview

This repository demonstrates a DevOps solution using **Ansible**, **Jenkins**, **Kubernetes**, and **Helm** to deploy a multi-language web application stack (NodeJS, Python, PHP) locally on Kubernetes (Minikube).

> **Note:** AWS provisioning steps are skipped due to no AWS account access. This focuses on local Kubernetes deployment and Jenkins CI/CD pipelines.

---

## Prerequisites

- [Minikube](https://minikube.sigs.k8s.io/docs/start/) installed and running
- [kubectl](https://kubernetes.io/docs/tasks/tools/) CLI configured for Minikube
- [Helm](https://helm.sh/docs/intro/install/) installed
- [Jenkins](https://www.jenkins.io/) deployed on Kubernetes (via Helm chart)
- [Ansible](https://docs.ansible.com/) installed locally (for running local playbooks)

---

## Setup Steps

### 1. Start Minikube

```bash
minikube start


**2. Deploy Jenkins on Minikube**

kubectl create namespace jenkins

helm repo add jenkins https://charts.jenkins.io
helm repo update

helm install jenkins jenkins/jenkins -n jenkins \
  --set controller.adminPassword='admin123' \
  --set controller.serviceType=NodePort

kubectl get svc -n jenkins jenkins
minikube ip

**3. Deploy the Kriyadocs Application Stack via Helm**

helm install kriyadocs-stack ./helm -n kriyadocs --create-namespace

kubectl get pods -n kriyadocs
kubectl get svc -n kriyadocs


**4. Access Applications**

kubectl port-forward svc/<service-name> 8080:80 -n kriyadocs
  ## Replace <service-name> with the specific app service (NodeJS, Python, PHP).

**5. Run Jenkins Pipeline**

Access Jenkins UI
Check for pipeline job named kriyadocs-pipeline
Run the pipeline and verify deployment logs

**Ansible Playbooks**
Currently, only local playbooks are included for environment setup.
AWS provisioning playbooks are omitted due to lack of AWS access.

ansible-playbook -i localhost, -c local playbooks/install-stack.yml


**NOTE: For any issues or questions, contact Praveen Kumar.**


