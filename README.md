# Terraform for DevOps — AWS Infrastructure (Hands-on Project)

This repository contains my hands-on implementation of AWS infrastructure using Terraform. The goal of this project was to understand Infrastructure as Code (IaC) in a real-world DevOps environment and practice building reusable, scalable, and maintainable cloud infrastructure.

---

## Overview

This project demonstrates how AWS infrastructure can be provisioned and managed using Terraform. It includes core services like EC2, S3, DynamoDB, and Amazon EKS, along with reusable modules and multi-environment support.

Instead of just learning Terraform syntax, this project focuses on how real DevOps teams structure infrastructure code in production systems.

---

## What I Built

In this project, I implemented the following:

- EC2 instances with security groups and SSH access
- S3 bucket with versioning and encryption
- DynamoDB table for state locking
- Remote backend configuration using S3 + DynamoDB
- Reusable Terraform modules for multiple environments
- EKS cluster setup with VPC networking
- Examples for advanced Terraform features like:
  - for_each loops
  - lifecycle rules
  - import existing resources
  - moved blocks for refactoring
  - terraform test framework

---

---

## 📸 Infrastructure Screenshots

Below are the actual AWS resources created using Terraform:

### EC2 Instance
<img width="1612" height="487" alt="Screenshot 2026-05-11 121550" src="https://github.com/user-attachments/assets/432d940c-1b41-4ce1-a79a-3270019818a5" />


### S3 Bucket
<img width="1062" height="520" alt="Screenshot 2026-05-11 121536" src="https://github.com/user-attachments/assets/5aa6a034-6824-48af-af8d-9e1a3d29cf35" />


### DynamoDB Table
<img width="1915" height="825" alt="Screenshot 2026-05-11 121629" src="https://github.com/user-attachments/assets/d4a68279-3f3d-4899-bbfc-b76fb43d09e6" />


### Terraform Apply Output
<img width="1920" height="1080" alt="Screenshot (141)" src="https://github.com/user-attachments/assets/e3580bd6-d859-4b21-a04f-ccfe5404d696" />


## Project Structure

```bash
terraform-for-devops/
├── terraform.tf          # Provider and version configuration
├── variables.tf          # Input variables
├── ec2.tf                # EC2 instance setup
├── s3.tf                 # S3 bucket configuration
├── dynamodb.tf          # DynamoDB table for state locking
├── outputs.tf           # Output values
├── script.sh            # EC2 bootstrap script
│
├── eks/                 # Amazon EKS cluster setup
│   ├── vpc.tf
│   ├── eks.tf
│   └── provider.tf
│
├── aws_module_project/  # Reusable Terraform modules
│   ├── main.tf
│   └── my_app_infra_module/
│
└── examples/            # Advanced Terraform concepts
    ├── for_each.tf
    ├── lifecycle.tf
    ├── import.tf
    ├── moved.tf
    ├── check.tf
    └── terraform_test/
