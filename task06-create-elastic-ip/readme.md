# 🌍 Task 06 — Allocate Elastic IP using Terraform

## 📌 Overview

In this task, I created an Elastic IP (EIP) using Terraform.
Elastic IPs are static public IPv4 addresses used to provide consistent access to cloud resources.

---

## 🎯 Objective

* Allocate an Elastic IP
* Name it **datacenter-eip**
* Use Terraform

---

## 🛠️ Terraform Configuration

```hcl
resource "aws_eip" "datacenter_eip" {
  domain = "vpc"

  tags = {
    Name = "datacenter-eip"
  }
}
```

---

## ⚙️ How It Works

* AWS automatically assigns a public IP
* Terraform manages it as a resource
* Tagging is used to identify the EIP

---

## 💡 Key Learning

Elastic IPs are not manually defined — they are allocated by AWS and managed using Terraform.
