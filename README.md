# 🚀 Terraform for DevOps — Hands-On AWS Infrastructure Repository

<p align="center">
  <img src="https://img.shields.io/badge/Terraform-v1.5+-7B42BC?style=for-the-badge&logo=terraform&logoColor=white"/>
  <img src="https://img.shields.io/badge/AWS-Cloud-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kubernetes-EKS-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white"/>
  <img src="https://img.shields.io/badge/DevOps-Infrastructure_as_Code-brightgreen?style=for-the-badge"/>
</p>

<p align="center">
  Production-style Infrastructure as Code (IaC) using Terraform, AWS, reusable modules, and Amazon EKS.
</p>

---

# 📌 Overview

This repository is a complete hands-on Terraform project designed for DevOps and Cloud Engineers who want to learn real-world Infrastructure as Code practices using AWS.

The project covers Terraform fundamentals all the way to advanced production-style workflows including:

- Reusable Terraform modules
- Multi-environment infrastructure
- Remote state management
- Amazon EKS cluster provisioning
- Infrastructure testing
- Advanced Terraform features and best practices

Instead of manually provisioning resources from the AWS Console, the entire infrastructure is automated and version controlled using Terraform.

---

# ⚡ Features

### ✅ AWS Infrastructure Provisioning
- EC2 Instances
- S3 Buckets
- DynamoDB Tables
- IAM Resources
- Security Groups
- VPC Networking

### ✅ Multi-Environment Deployments
Deploy separate:
- Development
- Staging
- Production

environments using reusable Terraform modules.

### ✅ Remote Terraform Backend
- Terraform state stored in Amazon S3
- State locking using DynamoDB

### ✅ Kubernetes Infrastructure
- Amazon EKS Cluster
- Managed Node Groups
- Public & Private Subnets
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

# 🛠️ Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/install) >= 1.5.0
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) configured with valid credentials
- AWS Account (Free Tier works for most examples)

---

# 🔢 Versions Used

| Tool | Version |
|------|---------|
| Terraform | >= 1.5.0 |
| AWS Provider | ~> 6.0 |
| EKS Module | ~> 21.0 |
| VPC Module | ~> 5.0 |

---

# 🏗️ Repository Structure

```bash
terraform-for-devops/
├── terraform.tf          # Provider config & version constraints
├── variables.tf          # Input variables with validation
├── ec2.tf                # EC2 instance, security group, key pair
├── s3.tf                 # S3 bucket with versioning & encryption
├── dynamodb.tf           # DynamoDB table
├── outputs.tf            # Output values
├── script.sh             # EC2 user_data bootstrap script
├── terra-key.pub         # SSH public key
│
├── eks/                  # EKS Cluster (v21.x module)
│   ├── provider.tf       # Provider + locals
│   ├── vpc.tf            # VPC module for EKS networking
│   └── eks.tf            # EKS cluster with managed node groups
│
├── aws_module_project/   # Reusable Modules example
│   ├── terraform.tf      # Provider version constraints
│   ├── providers.tf      # AWS provider region
│   ├── main.tf           # Module composition (dev, stg, prd)
│   └── my_app_infra_module/
│       ├── variables.tf  # Module inputs with validation
│       ├── my_server.tf  # EC2 instances (count)
│       ├── my_bucket.tf  # S3 bucket
│       ├── my_table.tf   # DynamoDB table
│       └── my_outputs.tf # Module outputs
│
└── examples/             # Modern Terraform feature examples
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

# 📚 What You'll Learn

| Concept | Location |
|---------|----------|
| Provider & version constraints | `terraform.tf` |
| Variables with validation | `variables.tf` |
| EC2, Security Groups, Key Pairs | `ec2.tf` |
| user_data bootstrapping | `script.sh` |
| S3 versioning & encryption | `s3.tf` |
| DynamoDB tables | `dynamodb.tf` |
| Outputs | `outputs.tf` |
| Reusable modules | `aws_module_project/` |
| Multi-environment deployments | `aws_module_project/main.tf` |
| Amazon EKS Cluster | `eks/` |
| VPC Networking | `eks/vpc.tf` |
| for_each & dynamic blocks | `examples/for_each.tf` |
| Lifecycle meta-arguments | `examples/lifecycle.tf` |
| Import existing resources | `examples/import.tf` |
| Resource refactoring | `examples/moved.tf` |
| Infrastructure assertions | `examples/check.tf` |
| Safe resource removal | `examples/removed.tf` |
| Terraform native testing | `examples/terraform_test/` |

---

# 🚀 Terraform Commands — Complete Guide

## 1️⃣ Setup & Initialization

### Install Terraform (Linux / Ubuntu)

```bash
wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install terraform

terraform -v
```

---

### Install Terraform (macOS)

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

---

### Initialize Terraform

```bash
terraform init
```

This command:
- Downloads provider plugins
- Initializes backend configuration
- Sets up the working directory

---

# 2️⃣ Core Terraform Commands

```bash
terraform fmt
terraform validate
terraform plan
terraform apply
terraform apply -auto-approve

terraform destroy
terraform destroy -auto-approve
```

| Command | Purpose |
|---|---|
| `terraform fmt` | Format Terraform files |
| `terraform validate` | Validate Terraform configuration |
| `terraform plan` | Preview infrastructure changes |
| `terraform apply` | Create/update infrastructure |
| `terraform destroy` | Remove infrastructure |

---

# 3️⃣ Managing Terraform State

```bash
terraform state list
terraform show
terraform state mv <src> <dest>
terraform state rm <resource>
```

### Remote Backend Configuration

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

---

# 4️⃣ Variables & Outputs

```bash
terraform apply -var="instance_type=t3.small"

terraform output

terraform output ec2_public_ip
```

---

# 5️⃣ Terraform Workspaces

```bash
terraform workspace new dev

terraform workspace select prod

terraform workspace list
```

---

# 6️⃣ Terraform Testing (Terraform 1.6+)

```bash
terraform test
```

Runs all `.tftest.hcl` files for infrastructure testing.

---

# 7️⃣ Debugging Terraform

```bash
export TF_LOG=DEBUG

terraform apply 2>&1 | tee debug.log
```

---

# ☸️ Amazon EKS Infrastructure

The `eks/` directory provisions:

- Amazon EKS Cluster
- Managed Node Groups
- Public & Private Subnets
- IAM Roles & Policies
- Kubernetes-ready networking

Deploy EKS:

```bash
cd eks/

terraform init

terraform apply
```

---

# 🌍 Multi-Environment Infrastructure

The `aws_module_project/` directory demonstrates reusable infrastructure modules for multiple environments.

| Environment | EC2 | S3 | DynamoDB |
|---|---|---|---|
| Development | 1× t3.micro | 1 Bucket | 1 Table |
| Staging | 1× t3.small | 1 Bucket | 1 Table |
| Production | 3× t3.medium | 2 Buckets | 1 Table |

Deploy environments individually:

```bash
cd aws_module_project/

terraform apply -target=module.dev

terraform apply -target=module.stg

terraform apply -target=module.prd
```

---

# 📖 Advanced Terraform Concepts

| Feature | Description |
|---|---|
| `for_each` | Dynamic resource creation |
| `validation` | Input validation |
| `lifecycle` | Infrastructure lifecycle management |
| `moved` | Safe resource refactoring |
| `import` | Import existing infrastructure |
| `check` | Infrastructure assertions |
| `removed` | Stop managing resources safely |
| `terraform test` | Native Terraform testing |

---

# 🎯 Future Improvements

- CI/CD using GitHub Actions
- CloudWatch Monitoring
- Helm Deployments
- Dockerized Workloads
- Security Hardening
- Terraform Cloud Integration

---

# 👨‍💻 Author

### Manish Mahalinge

DevOps | AWS | Terraform | Kubernetes | Cloud Infrastructure

---

# ⭐ Support

If you found this repository useful, consider giving it a star ⭐ on GitHub.

---

<p align="center">
  Built with Terraform • AWS • DevOps
</p>
