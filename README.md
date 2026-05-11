# 🚀 Terraform for DevOps — Hands-On AWS Infrastructure Repository

<p align="center">
  <img src="https://img.shields.io/badge/Terraform-v1.5+-7B42BC?style=for-the-badge&logo=terraform&logoColor=white"/>
  <img src="https://img.shields.io/badge/AWS-Cloud-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white"/>
  <img src="https://img.shields.io/badge/Kubernetes-EKS-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white"/>
  <img src="https://img.shields.io/badge/DevOps-IaC-brightgreen?style=for-the-badge"/>
</p>

<p align="center">
  A complete hands-on Terraform repository covering real AWS infrastructure, reusable modules, EKS, remote state management, and modern DevOps workflows.
</p>

---

# 📌 Overview

This repository is your one-stop solution for learning Terraform as a DevOps Engineer. It covers Terraform basics through advanced concepts using real AWS infrastructure and production-style Infrastructure as Code practices.

The project demonstrates how modern DevOps teams automate infrastructure provisioning using reusable Terraform modules, multi-environment deployments, remote state management, Kubernetes infrastructure, and scalable cloud architecture.

---

# ⚡ Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/install) >= 1.5.0 (recommended: 1.14.x)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) configured with valid credentials
- An AWS account (Free Tier works for most examples)

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
    ├── for_each.tf       # for_each & dynamic blocks
    ├── validation.tf     # Variable validation blocks
    ├── lifecycle.tf      # lifecycle meta-argument
    ├── moved.tf          # moved blocks (refactoring)
    ├── import.tf         # import blocks (Terraform 1.5+)
    ├── check.tf          # check blocks (continuous assertions)
    ├── removed.tf        # removed blocks (safe removal)
    └── terraform_test/   # Native terraform test (1.6+)
```

---

# 📚 What You'll Learn

| Concept | Where to Find It |
|---------|-----------------|
| Provider & version constraints | `terraform.tf` |
| Variables with validation | `variables.tf`, `examples/validation.tf` |
| EC2, Security Groups, Key Pairs | `ec2.tf` |
| user_data bootstrapping | `ec2.tf` + `script.sh` |
| S3 with versioning & encryption | `s3.tf` |
| DynamoDB tables | `dynamodb.tf` |
| Outputs | `outputs.tf` |
| Reusable modules | `aws_module_project/` |
| Multi-environment with modules | `aws_module_project/main.tf` |
| EKS cluster (v21.x) | `eks/` |
| VPC for Kubernetes | `eks/vpc.tf` |
| for_each & dynamic blocks | `examples/for_each.tf` |
| Lifecycle rules | `examples/lifecycle.tf` |
| Import existing resources | `examples/import.tf` |
| Refactoring with moved | `examples/moved.tf` |
| Continuous assertions | `examples/check.tf` |
| Safe resource removal | `examples/removed.tf` |
| terraform test framework | `examples/terraform_test/` |

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
- Sets up the working directory
- Initializes backend configuration

---

# ⚙️ Core Terraform Commands

```bash
terraform fmt
terraform validate
terraform plan
terraform apply
terraform apply -auto-approve

terraform destroy
terraform destroy -auto-approve
```

| Command | Description |
|---|---|
| `terraform fmt` | Format Terraform files |
| `terraform validate` | Validate configuration syntax |
| `terraform plan` | Preview infrastructure changes |
| `terraform apply` | Create/update infrastructure |
| `terraform destroy` | Remove infrastructure |

---

# 🗂️ Managing Terraform State

```bash
terraform state list
terraform show
terraform state mv <src> <dest>
terraform state rm <resource>
```

---

## 🔒 Remote Backend (S3 + DynamoDB Locking)

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

This setup helps prevent:
- State corruption
- Concurrent Terraform operations
- Infrastructure drift

---

# 📤 Variables & Outputs

```bash
terraform apply -var="instance_type=t3.small"

terraform output

terraform output ec2_public_ip
```

---

# 🌍 Terraform Workspaces

```bash
terraform workspace new dev

terraform workspace select prod

terraform workspace list
```

---

# 🧪 Terraform Testing (Terraform 1.6+)

```bash
terraform test
```

Runs all `.tftest.hcl` files.

---

# 🐞 Debugging Terraform

```bash
export TF_LOG=DEBUG

terraform apply 2>&1 | tee debug.log
```

---

# ☸️ Amazon EKS Infrastructure

The `eks/` directory provisions:

- Amazon EKS Cluster
- Managed Node Groups
- Kubernetes-ready VPC
- Public & Private Subnets
- IAM Roles & Policies

Deploy EKS:

```bash
cd eks/

terraform init

terraform apply
```

---

# 📖 Advanced Terraform Concepts Covered

| Feature | Description |
|---|---|
| `for_each` | Dynamic resource creation |
| `validation` | Input validation |
| `lifecycle` | Infrastructure lifecycle management |
| `moved` | Safe resource refactoring |
| `import` | Import existing infrastructure |
| `check` | Infrastructure assertions |
| `removed` | Safe resource decommissioning |
| `terraform test` | Native Terraform testing |

---

# 🎯 Future Improvements

- CI/CD using GitHub Actions
- Monitoring with CloudWatch
- Helm deployments on EKS
- Dockerized workloads
- Infrastructure security hardening
- Terraform Cloud integration

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
