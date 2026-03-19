# 🌐 Task 03 — Create VPC using Terraform

## 📌 Overview

In this task, I created a Virtual Private Cloud (VPC) using Terraform.
A VPC is the foundational networking component in AWS that allows you to isolate and manage your infrastructure.

---

## 🎯 Objective

* Create a VPC named **devops-vpc**
* Use any valid IPv4 CIDR block
* Deploy in **us-east-1 region**
* Use Terraform for provisioning

---

## 🛠️ Terraform Configuration

```hcl
resource "aws_vpc" "devops_vpc" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "devops-vpc"
  }
}
```

---

## ⚙️ How It Works (Most Important)

### 1. VPC Creation

* The `aws_vpc` resource creates a logically isolated network in AWS.
* It acts as the **base layer** for all networking resources like:

  * Subnets
  * EC2 instances
  * Load balancers

---

### 2. CIDR Block Explained

* `10.0.0.0/16` defines the IP range of the VPC
* It provides:

  * **65,536 IP addresses**
* This range can later be divided into smaller subnets

---

### 3. Tagging

* The `Name` tag helps identify the resource in AWS
* Makes management easier in real environments

---

## 🚀 Why This Matters

* ✅ Foundation for all AWS infrastructure
* ✅ Enables network isolation and control
* ✅ Required before creating subnets, routing, or EC2 resources
* ✅ Core concept for cloud and DevOps engineers

---

## 📂 Project Structure

```
task03-create-vpc/
├── README.md
└── main.tf
```

---

## ▶️ How to Run

```bash
cd /home/bob/terraform

terraform init
terraform plan
terraform apply -auto-approve
```

---

## 💡 Key Learning

This task demonstrates how to define cloud networking infrastructure using Terraform, forming the base for scalable and production-ready architectures.
