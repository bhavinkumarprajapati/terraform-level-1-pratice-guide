# 🌐 Task 05 — Create VPC with IPv6 using Terraform

## 📌 Overview

In this task, I created a VPC with both IPv4 and Amazon-provided IPv6 CIDR blocks using Terraform.

This is an important step toward building modern cloud infrastructure that supports IPv6 networking.

---

## 🎯 Objective

* Create a VPC named **devops-vpc**
* Enable **Amazon-provided IPv6 CIDR block**
* Deploy in **us-east-1 region**
* Use Terraform

---

## 🛠️ Terraform Configuration

```hcl
resource "aws_vpc" "devops_vpc" {
  cidr_block                       = "10.0.0.0/16"
  assign_generated_ipv6_cidr_block = true

  tags = {
    Name = "devops-vpc"
  }
}
```

---

## ⚙️ How It Works (Most Important)

### 1. Dual Stack VPC (IPv4 + IPv6)

* `cidr_block` → Defines IPv4 range
* `assign_generated_ipv6_cidr_block = true` → AWS automatically assigns an IPv6 range

👉 Result: The VPC supports **both IPv4 and IPv6**

---

### 2. What is Amazon-Provided IPv6?

* AWS automatically assigns a **/56 IPv6 block**
* You don’t need to manually define it
* It is globally unique and internet-routable

---

### 3. Why IPv6 Matters

* Massive address space (virtually unlimited)
* No need for NAT
* Better scalability for modern applications

---

### 4. Tagging

* The `Name` tag helps identify the VPC in AWS console

---

## 🚀 Why This Matters

* ✅ Modern cloud networking uses IPv6
* ✅ Required for large-scale distributed systems
* ✅ Important for future-proof infrastructure
* ✅ Frequently asked in DevOps interviews

---

## 📂 Project Structure

```
task05-create-vpc-ipv6/
├── README.md
└── main.tf
```

---

## ▶️ How to Run

```bash
cd /home/bob/terraform

terraform init
terraform apply -auto-approve
```

---

## 💡 Key Learning

This task demonstrates how to enable IPv6 in AWS VPCs using Terraform, allowing you to build scalable and future-ready cloud networks.
