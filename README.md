# 🚀 AWS Infrastructure Automation with Terraform

![Terraform](https://img.shields.io/badge/Terraform-v1.5+-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-Cloud-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![EKS](https://img.shields.io/badge/Kubernetes-EKS-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![IaC](https://img.shields.io/badge/IaC-Terraform-brightgreen?style=for-the-badge)

A production-style Infrastructure as Code (IaC) project built using Terraform and AWS.

This repository demonstrates how to provision and manage scalable cloud infrastructure across multiple environments using reusable Terraform modules, remote state management, Kubernetes (EKS), and modern Terraform best practices.

---

## 💡 Why I Built This

I got tired of manually clicking through the AWS console every time I needed to spin up infrastructure. Same EC2 settings, same S3 config, same security groups — over and over again.

I wanted to move beyond basic Terraform tutorials and build something closer to how infrastructure is managed in real DevOps environments. So I started automating everything with Terraform — EC2 instances, S3 buckets, networking, DynamoDB, and eventually Kubernetes infrastructure with EKS.

This project became my hands-on lab for learning:

- Infrastructure as Code
- Modular Terraform design
- Multi-environment deployments
- Remote state management
- Kubernetes provisioning on AWS
- Advanced Terraform workflows and testing

The goal was to build infrastructure the same way modern DevOps teams do in production.

---

## ⚡ What This Project Does

- ✔ Provisions AWS infrastructure using reusable Terraform modules
- ✔ Deploys separate Dev, Staging, and Production environments
- ✔ Uses S3 + DynamoDB for remote Terraform state management
- ✔ Creates an Amazon EKS cluster with managed node groups
- ✔ Demonstrates advanced Terraform features and best practices
- ✔ Organizes infrastructure using clean modular architecture
- ✔ Supports scalable and repeatable infrastructure deployments

---

## 🏗️ Architecture

```
                      ┌──────────────────────┐
                      │    Terraform IaC      │
                      │  (my_app_infra_module)│
                      └──────────┬───────────┘
             ┌────────────────────┼───────────────────┐
             ▼                    ▼                    ▼
      ┌─────────────┐    ┌─────────────┐    ┌──────────────┐
      │     Dev     │    │   Staging   │    │  Production  │
      │  1x EC2     │    │  1x EC2     │    │  3x EC2      │
      │  1x S3      │    │  1x S3      │    │  2x S3       │
      │  1x DynamoDB│    │  1x DynamoDB│    │  1x DynamoDB │
      └─────────────┘    └─────────────┘    └──────────────┘
                                  │
              ┌───────────────────▼──────────────────┐
              │         Remote State Backend          │
              │   S3 (terraform.tfstate) +            │
              │   DynamoDB (state lock)               │
              └───────────────────┬──────────────────┘
                                  │
              ┌───────────────────▼──────────────────┐
              │            EKS Cluster                │
              │   VPC · Private Subnets · Node Groups │
              └──────────────────────────────────────┘
```

---

## 🛠️ Core AWS Services Used

- EC2
- S3
- DynamoDB
- IAM
- VPC
- Security Groups
- Amazon EKS

---

## 📁 Repository Structure

```
aws-infrastructure-automation-terraform/
│
├── terraform.tf              # Provider config & version constraints
├── variables.tf              # Input variables with validation rules
├── ec2.tf                    # EC2 + security group + key pair
├── s3.tf                     # S3 bucket (versioning + encryption)
├── dynamodb.tf               # DynamoDB table
├── outputs.tf                # Output values
├── script.sh                 # EC2 user_data bootstrap script
│
├── eks/                      # Kubernetes cluster setup
│   ├── provider.tf
│   ├── vpc.tf                # VPC using terraform-aws-modules/vpc
│   └── eks.tf                # EKS cluster + managed node groups
│
├── aws_module_project/       # Multi-environment module usage
│   ├── main.tf               # Calls module for dev, stg, prd
│   └── my_app_infra_module/  # The reusable module itself
│       ├── variables.tf
│       ├── my_server.tf      # EC2 with count
│       ├── my_bucket.tf      # S3
│       ├── my_table.tf       # DynamoDB
│       └── my_outputs.tf
│
└── examples/                 # One file per advanced concept
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

## 🚀 Getting Started

### Prerequisites

- Terraform >= 1.5.0
- AWS CLI configured (`aws configure`)
- An AWS account — Free Tier is enough for most of this

### Quick Start

```bash
git clone https://github.com/<your-username>/aws-infrastructure-automation-terraform.git
cd aws-infrastructure-automation-terraform

terraform init
terraform plan
terraform apply
```

---

## 🌍 Multi-Environment Setup

The `aws_module_project/` folder shows how one module deploys three different environments.

```bash
cd aws_module_project/
terraform init
terraform apply -target=module.dev    # deploy dev only
terraform apply -target=module.stg   # deploy staging
terraform apply -target=module.prd   # deploy production
```

| Environment | EC2 | S3 | DynamoDB |
|-------------|-----|-----|----------|
| dev | 1× t3.micro | 1 bucket | 1 table |
| stg | 1× t3.small | 1 bucket | 1 table |
| prd | 3× t3.medium | 2 buckets | 1 table |

The only thing that changes between environments is the variable values passed into the module. The actual infra code stays the same.

---

## 🔒 Remote State Backend

Before I set this up, `terraform.tfstate` was sitting locally — fine for solo work, but a disaster waiting to happen in a team. Two people applying at the same time = corrupted state.

The fix: store state in S3 and use DynamoDB for locking.

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

## ☸️ EKS Cluster

```bash
cd eks/
terraform init
terraform apply
```

What gets created:
- VPC with public + private subnets (using `terraform-aws-modules/vpc`)
- EKS control plane (v1.35)
- Managed node groups with auto-scaling
- All required IAM roles and security groups

---

## 🔥 Key Terraform Concepts Covered

| File | Concept |
|------|---------|
| `for_each.tf` | Create multiple resources from a map/set — cleaner than `count` |
| `validation.tf` | Reject bad variable values before `apply` even runs |
| `lifecycle.tf` | `prevent_destroy`, `ignore_changes`, `create_before_destroy` |
| `import.tf` | Bring existing AWS resources under Terraform management |
| `moved.tf` | Rename resource in state without destroying and recreating it |
| `check.tf` | Assert conditions after deployment — like a health check |
| `removed.tf` | Stop managing a resource without deleting it from AWS |
| `terraform_test/` | Write and run unit tests for modules (Terraform 1.6+) |

---

## ⚙️ Useful Commands

```bash
# Core
terraform init          # download providers
terraform fmt           # auto-format all .tf files
terraform validate      # check for syntax errors
terraform plan          # preview what will change
terraform apply         # make it happen
terraform destroy       # tear it all down

# State
terraform state list                  # see all managed resources
terraform state mv <old> <new>        # rename in state
terraform state rm <resource>         # remove from state (not from AWS)

# Debug
export TF_LOG=DEBUG
terraform apply 2>&1 | tee debug.log

# Test (Terraform 1.6+)
terraform test
```

---

## 📚 What I Learned Building This

- Why `for_each` is almost always better than `count` for real infra
- How remote state locking prevents race conditions in team environments
- Why separating environments via modules beats workspaces for most use cases
- How to safely refactor Terraform code using `moved` blocks without destroying infra
- The difference between removing a resource from state vs actually destroying it
- How production infrastructure is structured in real DevOps workflows
- Best practices for scalable, maintainable Infrastructure as Code

---

## 🎯 Future Improvements

- CI/CD integration using GitHub Actions
- Monitoring with CloudWatch
- Helm deployments on EKS
- Dockerized application deployment
- Auto Scaling enhancements
- Infrastructure security hardening

---

## 🔢 Versions

| Tool | Version |
|------|---------|
| Terraform | >= 1.5.0 |
| AWS Provider | ~> 6.0 |
| EKS Module | ~> 21.0 |
| VPC Module | ~> 5.0 |

---

> If you're learning Terraform, clone this and break things. That's the best way.
