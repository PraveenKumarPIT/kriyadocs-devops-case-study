# Kriyadocs DevOps Case Study

This repo simulates a full DevOps pipeline using **Ansible**, **Jenkins**, **Docker**, **Helm**, and **Kubernetes**.

---

## Stack Simulated

- AWS VPC & EC2 provisioning via Ansible (simulated)
- Jenkins CI/CD
- Node.js, Python (Flask), PHP apps
- Deployed via Helm to local Minikube K8s cluster
- Docker-based builds
- Rancher-ready (optional)

---

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
````

---

### 2. Deploy Jenkins on Minikube

```bash
kubectl create namespace jenkins

helm repo add jenkins https://charts.jenkins.io
helm repo update

helm install jenkins jenkins/jenkins -n jenkins \
  --set controller.adminPassword='admin123' \
  --set controller.serviceType=NodePort

kubectl get svc -n jenkins jenkins
minikube ip
```

Access Jenkins UI at:
`http://<minikube-ip>:<node-port>`

Login credentials:

* **Username:** `admin`
* **Password:** `admin123`

---

### 3. Deploy the Kriyadocs Application Stack via Helm

```bash
helm install kriyadocs-stack ./helm -n kriyadocs --create-namespace

kubectl get pods -n kriyadocs
kubectl get svc -n kriyadocs
```

---

### 4. Access Applications

To access any deployed app (e.g., NodeJS, Python, PHP):

```bash
kubectl port-forward svc/<service-name> 8080:80 -n kriyadocs
```

Visit in browser:
[http://localhost:8080](http://localhost:8080)

> Replace `<service-name>` with the actual Kubernetes service name.

---

### 5. Run Jenkins Pipeline

* Access Jenkins UI.
* Locate the pipeline job named `kriyadocs-pipeline`.
* Run the pipeline and monitor deployment logs.

---

## Ansible Playbooks

Currently, only local setup playbooks are available (no AWS provisioning).

To run:

```bash
ansible-playbook -i localhost, -c local playbooks/install-stack.yml
```

## Contact

For any issues or questions, please contact **Praveen Kumar**.


