# 🔐 Task 01 — Create AWS Key Pair using Terraform

## 📌 Overview

In this task, I practiced creating an AWS EC2 key pair using Terraform as part of a step-by-step infrastructure migration approach.

Instead of manually creating keys, everything is defined as **Infrastructure as Code (IaC)** to ensure reproducibility and automation.

---

## 🎯 Objective

* Create a key pair named **devops-kp**
* Use **RSA algorithm**
* Store the private key securely at:

```bash
/home/bob/devops-kp.pem
```

---

## 🛠️ Terraform Configuration

```hcl
resource "tls_private_key" "devops_key" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

resource "aws_key_pair" "devops_kp" {
  key_name   = "devops-kp"
  public_key = tls_private_key.devops_key.public_key_openssh
}

resource "local_file" "private_key" {
  content         = tls_private_key.devops_key.private_key_pem
  filename        = "/home/bob/devops-kp.pem"
  file_permission = "0600"
}
```

---

## ⚙️ How It Works (Most Important)

This setup automates the complete lifecycle of an SSH key pair:

### 1. Generate Private Key

* The `tls_private_key` resource creates a **secure RSA key (4096 bits)**.
* This happens locally during Terraform execution.
* No manual key generation is required.

---

### 2. Extract Public Key

* Terraform automatically derives the **public key** from the generated private key.
* This ensures both keys are always in sync.

---

### 3. Create AWS Key Pair

* The `aws_key_pair` resource uploads the public key to AWS.
* This allows EC2 instances to use this key for SSH access.

---

### 4. Store Private Key Securely

* The `local_file` resource saves the private key to:

  ```
  /home/bob/devops-kp.pem
  ```
* File permission is set to **0600** (read/write only for owner), which is required for SSH.

---

## 🚀 Why This Approach Matters

* ✅ Fully automated (no manual SSH key creation)
* ✅ Reproducible across environments
* ✅ Secure key handling with proper permissions
* ✅ Aligns with DevOps and GitOps practices

---

## 📂 Project Structure

```
task01-create-keypair/
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

This task demonstrates how Terraform can manage not only cloud resources but also **local artifacts (like SSH keys)**, making it a powerful tool for end-to-end infrastructure automation.
