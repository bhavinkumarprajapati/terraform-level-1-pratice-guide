# 🖥️ Task 05— Create EC2 Instance using Terraform

## 📌 Overview

In this task, I provisioned an EC2 instance using Terraform, including automated key pair generation and secure access configuration.

---

## 🎯 Objective

* Launch EC2 instance with:

  * Name: **xfusion-ec2**
  * AMI: **ami-0c101f26f147fa7fd**
  * Instance type: **t2.micro**
* Create RSA key pair: **xfusion-kp**
* Attach default security group

---

## 🛠️ Terraform Configuration

```hcl id="q1h7n7"
# Fetch default VPC
data "aws_vpc" "default" {
  default = true
}

# Fetch default security group
data "aws_security_group" "default" {
  name   = "default"
  vpc_id = data.aws_vpc.default.id
}

# Generate RSA key
resource "tls_private_key" "xfusion_key" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

# Create AWS key pair
resource "aws_key_pair" "xfusion_kp" {
  key_name   = "xfusion-kp"
  public_key = tls_private_key.xfusion_key.public_key_openssh
}

# Create EC2 instance
resource "aws_instance" "xfusion_ec2" {
  ami           = "ami-0c101f26f147fa7fd"
  instance_type = "t2.micro"

  key_name = aws_key_pair.xfusion_kp.key_name

  vpc_security_group_ids = [
    data.aws_security_group.default.id
  ]

  tags = {
    Name = "xfusion-ec2"
  }
}
```

---

## ⚙️ How It Works (Most Important)

### 1. Key Pair Automation

* Generates RSA key using Terraform
* Automatically uploads public key to AWS

---

### 2. Default Network Usage

* Uses default VPC and security group
* Simplifies setup (no custom networking required)

---

### 3. EC2 Provisioning

* Launches instance using specified AMI
* Associates key pair for SSH access

---

## 🚀 Why This Matters

* ✅ Combines compute + security + access
* ✅ Fully automated infrastructure provisioning
* ✅ Real-world DevOps workflow
* ✅ Foundation for advanced setups (autoscaling, load balancing)

---

## 💡 Key Learning

Terraform can orchestrate multiple resources together (key pair + security + compute), enabling complete infrastructure automation.
