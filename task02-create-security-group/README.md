# 🔐 Task 02 — Create Security Group using Terraform

## 📌 Overview

In this task, I created an AWS Security Group using Terraform as part of incremental infrastructure provisioning.

Security groups act as virtual firewalls that control inbound and outbound traffic for AWS resources.

---

## 🎯 Objective

Create a security group with the following configuration:

* Name: **datacenter-sg**
* Description: **Security group for Nautilus App Servers**
* Allow inbound traffic:

  * HTTP (Port 80) from `0.0.0.0/0`
  * SSH (Port 22) from `0.0.0.0/0`
* Deploy in **default VPC** (us-east-1 region)

---

## 🛠️ Terraform Configuration

```hcl
resource "aws_security_group" "datacenter_sg" {
  name        = "datacenter-sg"
  description = "Security group for Nautilus App Servers"

  ingress {
    description = "Allow HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "Allow SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

---

## ⚙️ How It Works (Most Important)

### 1. Security Group Creation

* The `aws_security_group` resource creates a firewall inside AWS.
* It is automatically attached to the **default VPC** if no VPC is specified.

---

### 2. Inbound Rules (Ingress)

#### HTTP Rule

* Allows traffic on port **80**
* Used for web applications
* Open to all (`0.0.0.0/0`)

#### SSH Rule

* Allows traffic on port **22**
* Used for remote server access
* Open to all (`0.0.0.0/0`)

---

### 3. Outbound Rules (Egress)

* Allows all outbound traffic
* Required for instances to:

  * Access internet
  * Download packages
  * Communicate with other services

---

## 🚀 Why This Matters

* ✅ Demonstrates infrastructure security configuration using Terraform
* ✅ Reproducible and version-controlled firewall rules
* ✅ Essential for real-world DevOps and cloud environments
* ⚠️ Note: Opening SSH to `0.0.0.0/0` is not recommended in production

---

## 📂 Project Structure

```
task02-create-security-group/
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

This task highlights how Terraform can be used to define **network security rules as code**, making infrastructure safer, consistent, and easy to manage across environments.
