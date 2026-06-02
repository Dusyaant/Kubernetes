# Kubernetes Task: Local Cluster Isolation & Configuration

This repository documents the step-by-step implementation of setting up a local single-node Kubernetes cluster using Minikube on a cloud environment and creating dedicated cluster workspaces (Namespaces) for application isolation.

---

## 🛠️ Environment Stack & Prerequisites

* **Host Operating System:** Amazon Linux 2023 (AWS EC2 Instance)
* **Container Engine:** Docker Runtime
* **Orchestration Tool:** Minikube (v1.38.1)
* **Cluster Management CLI:** Kubectl

---

## 🚀 Step-by-Step Implementation

### 1. Host Machine Environment & Docker Initialization

To establish the underlying runtime platform, system dependencies were synchronized and the Docker engine was installed and configured.

```bash
sudo dnf update -y
sudo dnf install -y docker

sudo systemctl start docker
sudo systemctl enable docker

# Allow the current user to access Docker without sudo
sudo usermod -aG docker ec2-user
newgrp docker
```

---

### 2. Minikube Cluster Deployment

Due to memory constraints on the EC2 instance, Minikube was started with a reduced memory allocation of 900 MB and the validation checks were bypassed using the `--force` flag.

```bash
minikube start --driver=docker --memory=900mb --force
```

#### Verification: Cluster Boot Sequence

After startup, Minikube successfully:

* Pulled the required Kubernetes images
* Configured the Container Network Interface (CNI)
* Initialized cluster components
* Started the default storage provisioner

Verify cluster status:

```bash
minikube status
kubectl get nodes
```

---

### 3. Namespace Configuration & Verification

To isolate workloads and organize resources, a custom namespace named `devops-task` was created.

#### Create Namespace

```bash
kubectl create namespace devops-task
```

#### Verify Namespace Creation

```bash
kubectl get namespaces
```

Expected output includes:

* default
* devops-task
* kube-node-lease
* kube-public
* kube-system

This confirms that the custom workspace has been successfully created alongside the default Kubernetes system namespaces.

---

## 📋 Cluster Validation Commands

Check cluster information:

```bash
kubectl cluster-info
```

View available nodes:

```bash
kubectl get nodes
```

View all namespaces:

```bash
kubectl get ns
```

---

## 🧹 Session Teardown

To conserve EC2 resources after completing the task, the Minikube cluster was safely stopped.

```bash
minikube stop
```

---

## ✅ Task Outcome

Successfully configured:

* Docker runtime on Amazon Linux 2023
* Local Kubernetes cluster using Minikube
* Single-node Kubernetes environment
* Custom namespace (`devops-task`) for workload isolation
* Cluster verification and validation procedures
* Resource cleanup through controlled cluster shutdown

