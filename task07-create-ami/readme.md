# 🖼️ Task07 — Create AMI from EC2 Instance using Terraform

## 📌 Overview

In this task, I created an Amazon Machine Image (AMI) from an existing EC2 instance using Terraform.
AMIs are snapshots of an EC2 instance used to launch identical instances or preserve a machine's state.

---

## 🎯 Objective

* Provision an EC2 instance named **devops-ec2**
* Create an AMI named **devops-ec2-ami** from it
* Ensure the AMI reaches **available** state
* Use Terraform

---

## 🛠️ Terraform Configuration
```hcl
# Provision EC2 instance
resource "aws_instance" "ec2" {
  ami           = "ami-0c101f26f147fa7fd"
  instance_type = "t2.micro"
  vpc_security_group_ids = [
    "sg-c22bfd8f573c48e51"
  ]

  tags = {
    Name = "devops-ec2"
  }
}

# Create AMI from the EC2 instance
resource "aws_ami_from_instance" "devops_ec2_ami" {
  name               = "devops-ec2-ami"
  source_instance_id = aws_instance.ec2.id

  timeouts {
    create = "10m"
  }
}
```

---

## ⚙️ How It Works

* Terraform first provisions the EC2 instance with the specified AMI and instance type
* `aws_ami_from_instance` takes a snapshot of the running instance
* Terraform waits until the AMI reaches **available** state before completing
* The `source_instance_id` directly references the EC2 resource in the same configuration

---

## 💡 Key Learning

AMIs are created from existing instances — Terraform's `aws_ami_from_instance` handles the full lifecycle,
including waiting for the image to become available, making it reliable for automation pipelines.