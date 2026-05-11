# 🚀 AWS Infrastructure Automation with Terraform

<p align="center">
  <img src="https://img.shields.io/badge/Terraform-v1.5+-7B42BC?style=for-the-badge&logo=terraform&logoColor=white"/>
  <img src="https://img.shields.io/badge/AWS-Cloud-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kubernetes-EKS-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white"/>
  <img src="https://img.shields.io/badge/IaC-Infrastructure_as_Code-brightgreen?style=for-the-badge"/>
</p>

<p align="center">
  Production-style AWS Infrastructure Automation using Terraform, reusable modules, remote state management, and Amazon EKS.
</p>

---

# 📌 Overview

This repository demonstrates how modern cloud infrastructure can be provisioned and managed entirely through Infrastructure as Code (IaC) using Terraform and AWS.

The project follows real-world DevOps practices by implementing:

- Multi-environment infrastructure
- Reusable Terraform modules
- Remote state management
- Kubernetes infrastructure using Amazon EKS
- Modular and scalable architecture
- Advanced Terraform workflows

Instead of manually provisioning infrastructure from the AWS Console, everything is automated, version-controlled, and reproducible.

---

# ⚡ Key Features

### ✅ Infrastructure Provisioning
- EC2 instances
- S3 buckets
- DynamoDB tables
- Security Groups
- IAM resources
- VPC networking

### ✅ Multi-Environment Deployment
Deploy isolated:
- Development
- Staging
- Production

environments using the same reusable Terraform modules.

### ✅ Remote Terraform Backend
- Terraform state stored securely in Amazon S3
- State locking using DynamoDB

### ✅ Kubernetes Infrastructure
- Amazon EKS cluster
- Managed node groups
- VPC with public/private subnets
- Production-style networking

### ✅ Advanced Terraform Concepts
- `for_each`
- `lifecycle`
- `moved`
- `import`
- `check`
- Variable validation
- Native Terraform testing

---

# 🏗️ Infrastructure Architecture

```text
                      ┌─────────────────────────────┐
                      │      Terraform IaC          │
                      │   Reusable Infrastructure   │
                      │          Modules            │
                      └─────────────┬──────────────┘
                                    │
          ┌─────────────────────────┼─────────────────────────┐
          ▼                         ▼                         ▼
   ┌──────────────┐         ┌──────────────┐         ┌──────────────┐
   │ Development  │         │   Staging    │         │ Production   │
   │   1x EC2     │         │   1x EC2     │         │   3x EC2     │
   │   1x S3      │         │   1x S3      │         │   2x S3      │
   │ DynamoDB     │         │ DynamoDB     │         │ DynamoDB     │
   └──────────────┘         └──────────────┘         └──────────────┘
                                    │
                    ┌───────────────▼────────────────┐
                    │     Remote Terraform State      │
                    │     Amazon S3 + DynamoDB        │
                    └───────────────┬────────────────┘
                                    │
                    ┌───────────────▼────────────────┐
                    │         Amazon EKS              │
                    │ Kubernetes Cluster + NodeGroups │
                    └────────────────────────────────┘
```

---

# 🛠️ AWS Services Used

| Service | Purpose |
|---|---|
| Amazon EC2 | Compute infrastructure |
| Amazon S3 | Storage & Terraform backend |
| DynamoDB | Terraform state locking |
| IAM | Access management |
| VPC | Networking |
| Security Groups | Firewall rules |
| Amazon EKS | Kubernetes cluster |

---

# 📂 Repository Structure

```bash
aws-infrastructure-automation-terraform/
│
├── terraform.tf
├── variables.tf
├── ec2.tf
├── s3.tf
├── dynamodb.tf
├── outputs.tf
├── script.sh
│
├── eks/
│   ├── provider.tf
│   ├── vpc.tf
│   └── eks.tf
│
├── aws_module_project/
│   ├── main.tf
│   └── my_app_infra_module/
│
└── examples/
    ├── for_each.tf
    ├── validation.tf
    ├── lifecycle.tf
    ├── moved.tf
    ├── import.tf
    ├── check.tf
    ├── removed.tf
    └── terraform_test/
```

---

# 🚀 Getting Started

## Prerequisites

- Terraform >= 1.5.0
- AWS CLI configured
- AWS account

---

## Clone Repository

```bash
git clone https://github.com/manish-mahalinge/aws-infrastructure-automation-terraform.git

cd aws-infrastructure-automation-terraform
```

---

## Initialize Terraform

```bash
terraform init
```

---

## Validate Configuration

```bash
terraform validate
```

---

## Preview Infrastructure

```bash
terraform plan
```

---

## Deploy Infrastructure

```bash
terraform apply
```

---

# 🌍 Multi-Environment Deployment

The `aws_module_project/` directory demonstrates reusable infrastructure modules for multiple environments.

| Environment | EC2 | S3 | DynamoDB |
|---|---|---|---|
| Development | 1× t3.micro | 1 Bucket | 1 Table |
| Staging | 1× t3.small | 1 Bucket | 1 Table |
| Production | 3× t3.medium | 2 Buckets | 1 Table |

Example:

```bash
cd aws_module_project/

terraform init

terraform apply -target=module.dev
terraform apply -target=module.stg
terraform apply -target=module.prd
```

---

# 🔒 Remote State Management

Terraform state is securely stored using:

- Amazon S3 → State Storage
- DynamoDB → State Locking

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "global/s3/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-lock"
    encrypt        = true
  }
}
```

This prevents:
- State corruption
- Concurrent Terraform runs
- Infrastructure drift

---

# ☸️ Amazon EKS Cluster

The `eks/` directory provisions:

- Amazon EKS Cluster
- Managed Node Groups
- Kubernetes-ready VPC
- Public & Private Subnets
- IAM Roles & Policies
- Autoscaling Worker Nodes

Deploy EKS:

```bash
cd eks/

terraform init
terraform apply
```

---

# 🔥 Terraform Concepts Demonstrated

| File | Concept |
|---|---|
| `for_each.tf` | Dynamic resource creation |
| `validation.tf` | Variable validation |
| `lifecycle.tf` | Lifecycle meta-arguments |
| `import.tf` | Importing existing infrastructure |
| `moved.tf` | Safe resource refactoring |
| `check.tf` | Infrastructure assertions |
| `removed.tf` | Safe resource decommissioning |
| `terraform_test/` | Native Terraform testing |

---

# ⚙️ Common Terraform Commands

```bash
# Initialize
terraform init

# Format files
terraform fmt

# Validate configuration
terraform validate

# Preview changes
terraform plan

# Apply changes
terraform apply

# Destroy infrastructure
terraform destroy

# Terraform State
terraform state list
terraform state mv <old> <new>
terraform state rm <resource>

# Workspaces
terraform workspace list
terraform workspace new dev

# Testing
terraform test
```

---

# 📚 What I Learned

- Designing reusable Terraform modules
- Infrastructure automation best practices
- Managing remote Terraform state
- Deploying production-style AWS infrastructure
- Kubernetes provisioning with Amazon EKS
- Terraform testing & validation
- Safe infrastructure refactoring
- Multi-environment infrastructure design

---

# 🎯 Future Improvements

- GitHub Actions CI/CD
- Helm deployments
- Monitoring with CloudWatch
- Dockerized workloads
- Infrastructure security hardening
- Terraform Cloud integration

---

# 🔢 Versions

| Tool | Version |
|---|---|
| Terraform | >= 1.5.0 |
| AWS Provider | ~> 6.0 |
| EKS Module | ~> 21.0 |
| VPC Module | ~> 5.0 |

---

# 👨‍💻 Author

### Manish Mahalinge

DevOps | Cloud | Terraform | AWS | Kubernetes

---

# ⭐ Support

If you found this project useful, consider giving it a star ⭐ on GitHub.
