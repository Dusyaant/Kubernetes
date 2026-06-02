# Kubernetes Task: Local Cluster Isolation & Configuration

This repository documents the step-by-step implementation of setting up a local single-node Kubernetes cluster using Minikube on a cloud environment and creating dedicated cluster workspaces (Namespaces) for application isolation.

## 🛠️ Environment Stack & Prerequisites
* **Host Operating System:** Amazon Linux 2023 (AWS EC2 Instance)
* **Container Engine:** Docker Runtime
* **Orchestration Tool:** Minikube (v1.38.1)
* **Cluster Management CLI:** Kubectl

---

## 🚀 Step-by-Step Implementation

### 1. Host Machine Environment & Docker Initialization
To establish the underlying runtime platform, system dependencies were synchronized and the native Docker engine package was provisioned:
```bash
sudo dnf update -y
sudo dnf install -y docker
sudo systemctl start docker
sudo systemctl enable docker

# Authorize user to interface with docker socket without superuser elevation
sudo usermod -aG docker ec2-user
newgrp docker
