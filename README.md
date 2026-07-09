# 🚀 Terraform Capstone Project

## 📖 Project Overview  
The Terraform Capstone Project automates the deployment of AWS resources including EC2, S3, and DynamoDB. This project demonstrates practical use of Terraform to create a scalable architecture across multiple environments.

## 🏗️ Architecture  
The architecture consists of various AWS services integrated to work seamlessly.
- **EC2 Instances**: Used to run applications.
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
