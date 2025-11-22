# 🚀 End-to-End Kubernetes Task Manager Project

This project demonstrates a **Full Stack Microservices Application** deployed on **Kubernetes (Minikube)** using **Helm Charts** for automation.

It simulates a real-world production environment including Frontend, Backend, Database with persistence, and Ingress routing.

## 🏗️ Architecture



The application is composed of the following microservices:

1.  **Frontend:** Apache Web Server (`httpd:alpine`) acting as the UI.
2.  **Backend:** Nginx Server (`nginx:alpine`) acting as the API Gateway.
3.  **Database:** MongoDB (`mongo:5.0`) with **Persistent Volume Claims (PVC)** to ensure data survival.
4.  **Ingress Controller:** Nginx Ingress for smart traffic routing (`/` → Frontend, `/api` → Backend).
5.  **Configuration:** Managed via **ConfigMaps** and **Secrets** (Base64 encoded credentials).

---

## 🛠️ Prerequisites

Before running this project, ensure you have the following installed:

* **Docker Desktop** (Container Runtime)
* **Minikube** (Local Kubernetes Cluster)
* **Kubectl** (Kubernetes CLI)
* **Helm** (Kubernetes Package Manager)

---

## 📂 Project Structure

```text
k8s-task-manager/
├── task-app-chart/       # The Helm Chart (Automation Logic)
│   ├── templates/        # Dynamic YAML Manifests
│   ├── Chart.yaml        # Chart Metadata
│   └── values.yaml       # Control Panel (Variables)
└── README.md             # Documentation

## 🚀 Quick Start Guide

Follow these steps to deploy the application from scratch.

### Step 1: Start Minikube

Start the cluster and enable the Ingress Controller.

```bash
minikube start --driver=docker
minikube addons enable ingress
```

> **Important:** Open a **New Terminal (Administrator)** and run the tunnel command to assign an External IP. Keep this terminal running.

```bash
minikube tunnel
```

### Step 2: Install the Application (Using Helm)

Deploy the entire stack (Frontend + Backend + Database) with a single command.

```bash
# Navigate to project folder
cd k8s-task-manager

# Install the Chart
helm install my-task-app ./task-app-chart
```

### Step 3: Verify Deployment

Check if all pods are up and running.

```bash
kubectl get pods
```

*Expected Output: You should see Frontend, Backend, and Mongo-DB pods in `Running` state.*

-----

## 🌐 Networking & Access

Since we are running locally, we need to map the domain to our local cluster.

### Update Hosts File

1.  **Windows:** Open Notepad as Administrator and edit `C:\Windows\System32\drivers\etc\hosts`.
2.  **Linux/Mac:** Edit `/etc/hosts`.

Add the following line at the end:

```text
127.0.0.1  task-app.test
```

### Access the App

Open your browser and visit:

  * **Frontend UI:** [http://task-app.test](https://www.google.com/search?q=http://task-app.test)
  * **Backend API:** [http://task-app.test/api](https://www.google.com/search?q=http://task-app.test/api)

-----

## ⚡ Scaling (The Power of Helm)

Need to handle more traffic? You can scale the Frontend replicas instantly without editing files.

```bash
# Scale Frontend to 5 Replicas
helm upgrade my-task-app ./task-app-chart --set replicaCount=5
```

Verify the scaling:

```bash
kubectl get pods
```

```
```# kubernetes-fullstack-helm-demo
