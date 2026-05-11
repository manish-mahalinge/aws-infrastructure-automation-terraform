# 🚀 Terraform for DevOps — AWS Infrastructure (Hands-on Project)

This repository demonstrates real-world Infrastructure as Code (IaC) using Terraform to provision and manage AWS infrastructure in a scalable and production-style manner.

The project focuses on understanding how DevOps teams design, automate, and manage cloud infrastructure using best practices.

---

## 📌 Overview

This project automates AWS infrastructure provisioning using Terraform and includes core AWS services:

- EC2 for compute
- S3 for storage
- DynamoDB for state locking
- Reusable modules using Terraform module structure

The goal is to implement Infrastructure as Code in a clean, modular, and maintainable way.

---

## 🛠️ Prerequisites

- Terraform >= 1.5.0  
- AWS CLI configured with valid credentials  
- AWS account (Free Tier is sufficient)

---

## 🏗️ Project Structure

terraform-for-devops/
├── terraform.tf          # Provider & version configuration
├── variables.tf          # Input variables with validation
├── ec2.tf                # EC2 instance setup
├── s3.tf                 # S3 bucket configuration
├── dynamodb.tf           # DynamoDB table for state locking
├── outputs.tf            # Output values
│
├── aws_module_project/   # Reusable Terraform modules
│   ├── main.tf
│   └── my_app_infra_module/

---

## 📚 What You’ll Learn

• AWS infrastructure provisioning using Terraform  
• EC2 instance creation and configuration  
• S3 bucket setup with best practices  
• DynamoDB for Terraform state locking  
• Modular infrastructure design using Terraform modules  
• Variables and outputs management in Terraform  

---

## ⚙️ Core Terraform Commands

terraform init  
terraform fmt  
terraform validate  
terraform plan  
terraform apply  
terraform destroy  

---

## 🧠 State Management (Important)

terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "global/s3/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-lock"
    encrypt        = true
  }
}

---

## 🚀 Key Highlights

• Real AWS infrastructure automation using Terraform  
• Modular and reusable infrastructure design  
• Secure state management using S3 + DynamoDB locking  
• Clean separation of resources and configuration  
• Production-style Infrastructure as Code practices  

---

## 🎯 Goal of This Project

To build a practical understanding of Infrastructure as Code (IaC) by automating AWS infrastructure in a modular and production-style approach using Terraform.
