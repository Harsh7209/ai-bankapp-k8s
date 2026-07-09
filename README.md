# 🚀 Terraform Capstone Project

## 📖 Project Overview  
The Terraform Capstone Project automates the deployment of AWS resources including EC2, S3, and DynamoDB. This project demonstrates practical use of Terraform to create a scalable architecture across multiple environments.

## 🏗️ Architecture  
The architecture consists of various AWS services integrated to work seamlessly.
- **EC2 Instances**: Used to run applications.# 🚀 AI Bank App - Kubernetes Deployment (KIND)

## 📌 Project Background

This project is based on an open-source banking application that I adopted and extended.

I enhanced the project by:
- Adding Kubernetes (K8s) configuration files
- Containerizing the application using Docker
- Deploying the application using a Kubernetes cluster created with KIND (Kubernetes IN Docker)
- Implementing a full **DevSecOps CI/CD pipeline** with security checks, image scanning, and automated Docker Hub publishing

---

## 🧱 Tech Stack

- Docker
- Kubernetes
- KIND (Kubernetes IN Docker)
- GitHub Actions (CI/CD)
- Trivy (Image & Filesystem Scanning)
- GitLeaks (Secret Detection)
- Hadolint (Dockerfile Linting)
- OWASP Dependency Check
- Spring Boot (Application)

---

## 🔐 DevSecOps Pipeline

The project includes a full **DevSecOps CI/CD pipeline** implemented using GitHub Actions. Security is integrated at every stage — from code commit to Docker Hub push — following the **"Shift Left"** security philosophy.

### 🔄 Pipeline Stages Overview

```
Code Push
    │
    ▼
┌─────────────────────┐
│  1. Lint Check       │  ← Code quality & style
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  2. GitLeaks Check   │  ← Secret & credential detection
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  3. Packages Check   │  ← Dependency vulnerability scan (OWASP)
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  4. Dockerfile Check │  ← Dockerfile best practices (Hadolint)
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  5. Image Scan       │  ← Container image scan (Trivy)
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│  6. Build & Push     │  ← Build Docker image & push to Docker Hub
└─────────────────────┘
```

---

### 🧹 Stage 1 — Lint Check

Runs static code analysis to enforce code quality and catch common issues early.

- Checks for code style violations
- Flags syntax issues and anti-patterns
- Fails the pipeline if linting errors are found

---

### 🔑 Stage 2 — GitLeaks Check

Uses **[GitLeaks](https://github.com/gitleaks/gitleaks)** to scan the entire repository for accidentally committed secrets and sensitive data.

**Detects:**
- API keys & tokens
- Passwords & credentials
- Private keys & certificates
- Cloud provider secrets (AWS, GCP, Azure)

```yaml
- name: Run GitLeaks
  uses: gitleaks/gitleaks-action@v2
```

> ⚠️ Pipeline fails immediately if any secrets are detected.

---

### 📦 Stage 3 — Packages Check

Uses **OWASP Dependency Check** to scan all project dependencies for known CVEs (Common Vulnerabilities and Exposures).

- Scans Maven/Gradle/npm dependencies
- Cross-references against the **NVD (National Vulnerability Database)**
- Generates a detailed vulnerability report
- Fails on HIGH or CRITICAL severity findings

```yaml
- name: Run OWASP Dependency Check
  uses: dependency-check/Dependency-Check_Action@main
```

---

### 🐳 Stage 4 — Dockerfile Check

Uses **[Hadolint](https://github.com/hadolint/hadolint)** to lint the `Dockerfile` and ensure it follows best practices.

**Checks include:**
- Using specific image tags instead of `latest`
- Combining `RUN` commands to reduce layers
- Avoiding `sudo` usage
- Correct `COPY` vs `ADD` usage
- Security hardening recommendations

```yaml
- name: Lint Dockerfile
  uses: hadolint/hadolint-action@v3.1.0
  with:
    dockerfile: Dockerfile
```

---

### 🛡️ Stage 5 — Image Scan (Trivy)

Uses **[Trivy](https://github.com/aquasecurity/trivy)** by Aqua Security to scan the built Docker image for OS and application-level vulnerabilities.

**Scans for:**
- OS package vulnerabilities (Alpine, Ubuntu, Debian, etc.)
- Application dependency vulnerabilities
- Misconfigurations
- Secret exposure inside the image

```yaml
- name: Run Trivy vulnerability scanner
  uses: aquasecurity/trivy-action@master
  with:
    image-ref: bankapp:latest
    format: table
    severity: CRITICAL,HIGH
    exit-code: '1'
```

> ⚠️ Pipeline fails if CRITICAL or HIGH vulnerabilities are found in the image.

---

### 🚢 Stage 6 — Build & Push to Docker Hub

After all security checks pass, the Docker image is built and pushed to **Docker Hub** automatically.

```yaml
- name: Build Docker image
  run: docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/bankapp:latest .

- name: Push to Docker Hub
  run: docker push ${{ secrets.DOCKERHUB_USERNAME }}/bankapp:latest
```

**Required GitHub Secrets:**

| Secret | Description |
|--------|-------------|
| `DOCKERHUB_USERNAME` | Your Docker Hub username |
| `DOCKERHUB_TOKEN` | Docker Hub access token (not password) |

---

## ☸️ Kubernetes Implementation

I created a `k8s/` folder that contains all the Kubernetes manifests required to deploy the application.

### 🔧 Deployment

- Manages application pods
- Ensures desired number of replicas
- Automatically restarts failed containers

### 🌐 Service

- Exposes the application
- Routes traffic to the pods
- Enables internal/external access

---

## 🚀 Deployment Steps (Using KIND)

### 1️⃣ Create KIND Cluster

```bash
kind create cluster --name bankapp-cluster
```

### 2️⃣ Build Docker Image

```bash
docker build -t bankapp .
```

### 3️⃣ Load Image into KIND

```bash
kind load docker-image bankapp --name bankapp-cluster
```

### 4️⃣ Deploy to Kubernetes

```bash
kubectl apply -f k8s/
```

### 5️⃣ Verify

```bash
kubectl get pods
kubectl get svc
```

---

## 📁 Project Structure

```
.
├── .github/
│   └── workflows/
│       └── devsecops-pipeline.yml   # CI/CD pipeline definition
├── k8s/
│   ├── deployment.yaml              # Kubernetes Deployment manifest
│   └── service.yaml                 # Kubernetes Service manifest
├── src/                             # Application source code
├── Dockerfile                       # Container build instructions
└── README.md
```

---

## 💡 Summary

- Picked an open-source banking project
- Added Kubernetes configuration for container orchestration
- Used KIND to create a local Kubernetes cluster
- Deployed the application successfully on Kubernetes
- Implemented a **full DevSecOps pipeline** including:
  - ✅ Lint Check
  - ✅ GitLeaks secret scanning
  - ✅ OWASP Dependency vulnerability check
  - ✅ Dockerfile best-practice linting (Hadolint)
  - ✅ Container image scanning (Trivy)
  - ✅ Automated build & push to Docker Hub

---

## 👨‍💻 Author

**Harsh Choubey**

- **S3 Buckets**: For storing application data and backup.
- **DynamoDB**: NoSQL database for storing application state.

## 📂 Project Structure  
```
terraform-capstone/
├── main.tf              # Main Terraform configuration
├── variables.tf         # Input variables
├── outputs.tf           # Outputs after deployment
├── modules/             # Contains reusable modules
│   ├── ec2/             # EC2 module
│   ├── s3/              # S3 module
│   └── dynamodb/        # DynamoDB module
└── env/                # Environment specific configurations
    ├── dev/
    ├── stg/
    └── prod/
``` 

## 🔧 Prerequisites  
- AWS Account  
- Terraform installed on your local machine  
- AWS CLI configured  

## 🏁 Getting Started Guide  
### Step-by-Step Instructions  
1. Clone the repository:  
   ```bash  
   git clone https://github.com/Harsh7209/terraform-capstone.git  
   ```  
2. Navigate to the project directory:  
   ```bash  
   cd terraform-capstone  
   ```  
3. Initialize Terraform:  
   ```bash  
   terraform init  
   ```  
4. Plan your deployment:  
   ```bash  
   terraform plan  
   ```  
5. Apply the changes:  
   ```bash  
   terraform apply  
   ```  

## 🌍 Environment Configuration  
| Environment | EC2 Instance Type | S3 Bucket Name      | DynamoDB Table Name |  
|-------------|-------------------|----------------------|----------------------|  
| Dev         | t2.micro          | dev-bucket           | dev-table            |  
| Staging     | t2.medium         | stg-bucket           | stg-table            |  
| Production   | t2.large          | prod-bucket          | prod-table           |  

## 🔧 Troubleshooting
# Issue: "Provider AWS not found"
Solution: Run terraform init to download the AWS provider.

# Issue: "Invalid provider version"
Solution: Update AWS provider version in terraform.tf or run:

# Bash
terraform init -upgrade 

Issue: "Workspace does not exist" 

Solution: Create the workspace first:

# Bash
terraform workspace new <workspace-name> 

Issue: "Insufficient permissions" 

Solution: Verify AWS credentials:  

# Bash
aws sts get-caller-identity 

Ensure your IAM user has EC2, S3, and DynamoDB permissions.

# Issue: "Resource already exists"
Solution: Check AWS Console for existing resources 

# Bash
terraform destroy
terraform apply
Issue: "Invalid SSH key"
Solution: Update the public key in modules/ec2/main.tf



## ✨ Key Features

# 1. Multi-Environment Support
Dev, Staging, and Production environments
Independent state per environment using workspaces
Automatic scaling based on environment

# 2. Modular Design
Reusable EC2, S3, and DynamoDB modules
Each module is self-contained with its own variables
Easy to add new modules

# 3. Scalability
Use count parameter for dynamic resource creation
Simple variable adjustment for resource scaling
Supports adding new environments easily
 # 4. Security
Security group with SSH, HTTP, and HTTPS access
Key pair for secure EC2 access
DynamoDB with PAY_PER_REQUEST billing (no unused capacity)
 # 5. Naming Convention
Environment-based resource naming (e.g., dev-terra-server-1)
Consistent tagging across all resources
Easy resource identification in AWS Console
# 6. Cost Optimization
t3.micro instances (cost-effective)
Configurable resource counts per environment
DynamoDB PAY_PER_REQUEST billing


## 🥇 Best Practices  
- Use version control for your Terraform scripts.  
- Regularly update your modules to include security patches.  



## 🚀 Future Enhancements  
- Integration with CI/CD pipelines  
- Add more AWS services like RDS and Lambda  

## 👤 Author Information  
- **Name**: Harsh  
- **GitHub**: [Harsh7209](https://github.com/Harsh7209)  
- **Email**: harshchoubey113@example.com  

---  
This README is intended to provide all necessary information for deploying and using the resources configured through the Terraform Capstone project effectively.
