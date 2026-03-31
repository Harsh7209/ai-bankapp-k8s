# 🚀 AI Bank App - Kubernetes Deployment (KIND)

## 📌 Project Background

This project is based on an open-source banking application that I
adopted and extended.

I enhanced the project by: - Adding Kubernetes (K8s) configuration
files - Containerizing the application using Docker - Deploying the
application using a Kubernetes cluster created with KIND (Kubernetes IN
Docker)

------------------------------------------------------------------------

## 🧱 Tech Stack

-   Docker
-   Kubernetes
-   KIND (Kubernetes IN Docker)
-   (Application: Spring Boot / Node / etc.)

------------------------------------------------------------------------

## ☸️ Kubernetes Implementation

I created a `k8s/` folder that contains all the Kubernetes manifests
required to deploy the application.

### 🔧 Deployment

-   Manages application pods
-   Ensures desired number of replicas
-   Automatically restarts failed containers

### 🌐 Service

-   Exposes the application
-   Routes traffic to the pods
-   Enables internal/external access

------------------------------------------------------------------------

## 🚀 Deployment Steps (Using KIND)

### 1️⃣ Create KIND Cluster

``` bash
kind create cluster --name bankapp-cluster
```

### 2️⃣ Build Docker Image

``` bash
docker build -t bankapp .
```

### 3️⃣ Load Image into KIND

``` bash
kind load docker-image bankapp --name bankapp-cluster
```

### 4️⃣ Deploy to Kubernetes

``` bash
kubectl apply -f k8s/
```

### 5️⃣ Verify

``` bash
kubectl get pods
kubectl get svc
```

------------------------------------------------------------------------

## 💡 Summary

-   Picked an open-source project
-   Added Kubernetes configuration
-   Used KIND to create a local Kubernetes cluster
-   Deployed the application successfully

------------------------------------------------------------------------

## 👨‍💻 Author

Harsh Choubey
