# Highly Available Web Application on AWS with Terraform

![Terraform](https://img.shields.io/badge/IaC-Terraform-623CE4?logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/Cloud-AWS-FF9900?logo=amazonaws&logoColor=white)
![EC2](https://img.shields.io/badge/Compute-EC2-orange)
![ALB](https://img.shields.io/badge/Load%20Balancer-Application%20Load%20Balancer-blue)
![Auto Scaling](https://img.shields.io/badge/High%20Availability-Auto%20Scaling-success)
![License](https://img.shields.io/badge/License-MIT-green)

## Overview

This project provisions a **highly available Apache web application** on AWS using **Terraform**. The infrastructure follows AWS best practices by distributing traffic through an **Application Load Balancer (ALB)** and maintaining application availability with an **Auto Scaling Group (ASG)**.

Instead of manually provisioning infrastructure through the AWS Management Console, the entire environment is defined as **Infrastructure as Code (IaC)**, enabling repeatable, consistent, and version-controlled deployments.

---

# Business Problem

A growing web application cannot rely on a single EC2 instance because it introduces several operational risks:

- Single point of failure
- Downtime during maintenance or instance failure
- Inability to handle increasing traffic
- Manual infrastructure provisioning
- Configuration drift between environments

The business requires an infrastructure that is:

- Highly available
- Fault tolerant
- Easily reproducible
- Scalable
- Managed as code

---

# Solution

Terraform was used to provision an AWS infrastructure consisting of:

- Application Load Balancer
- Launch Template
- Auto Scaling Group
- Security Groups
- Default VPC and Subnets
- Apache Web Server
- Dynamic Amazon Linux 2023 AMI lookup

The solution ensures that traffic is distributed across healthy EC2 instances while automatically replacing unhealthy instances.

---

# Architecture

> **Architecture Diagram**

```
                    Internet
                        │
                        ▼
         Application Load Balancer
                        │
                HTTP Listener (80)
                        │
                        ▼
                 Target Group
                        │
          ┌─────────────┴─────────────┐
          ▼                           ▼
     EC2 Instance               EC2 Instance
          ▲                           ▲
          └─────────────┬─────────────┘
                        │
             Auto Scaling Group
                        │
               Launch Template
                        │
               Amazon Linux 2023
                        │
                  Apache Web Server
```

*A graphical architecture diagram is available in the `/diagrams` directory.*

---

# Technologies Used

- Terraform
- AWS EC2
- AWS Application Load Balancer
- AWS Auto Scaling
- AWS Security Groups
- AWS VPC
- Amazon Linux 2023
- Apache HTTP Server
- Git
- GitHub

---

# Project Structure

```text
highly-available-web-app-terraform/
│
├── terraform/
│   ├── providers.tf
│   ├── variables.tf
│   ├── networking.tf
│   ├── security.tf
│   ├── launch-template.tf
│   ├── alb.tf
│   ├── autoscaling.tf
│   ├── outputs.tf
│   ├── userdata.sh
│   ├── terraform.tfvars.example
│   └── .terraform.lock.hcl
│
├── docs/
├── diagrams/
├── screenshots/
└── README.md
```

---

# Infrastructure Components

## Networking

- Default AWS VPC
- Default Subnets across multiple Availability Zones

Terraform retrieves these resources using **data sources** instead of creating new networking infrastructure.

---

## Security

Two Security Groups were created following the Principle of Least Privilege.

### Application Load Balancer Security Group

- HTTP (80) from Internet
- Outbound traffic allowed

### EC2 Security Group

- HTTP only from the ALB Security Group
- SSH only from the administrator's public IP
- Outbound traffic allowed

This prevents direct public access to the EC2 instances.

---

## Compute

A Launch Template defines:

- Amazon Linux 2023
- Instance Type
- User Data
- Security Group
- Key Pair

The Auto Scaling Group uses this template to launch identical EC2 instances.

---

## Load Balancing

The Application Load Balancer:

- Receives incoming HTTP requests
- Performs health checks
- Routes traffic only to healthy EC2 instances
- Distributes requests across multiple Availability Zones

---

## Auto Scaling

The Auto Scaling Group:

- Maintains the desired number of EC2 instances
- Replaces unhealthy instances automatically
- Supports dynamic scaling using CPU utilization

---

# Deployment

Initialize Terraform:

```bash
terraform init
```

Format configuration:

```bash
terraform fmt
```

Validate configuration:

```bash
terraform validate
```

Review execution plan:

```bash
terraform plan
```

Deploy infrastructure:

```bash
terraform apply
```

Destroy infrastructure:

```bash
terraform destroy
```

---

# Validation

The deployment was validated by confirming:

- Application Load Balancer created successfully
- Target Group reports healthy targets
- Auto Scaling Group launched the desired number of instances
- Apache installed automatically through User Data
- Web application accessible through the ALB DNS name
- Unhealthy instances automatically replaced by the Auto Scaling Group

---

# Security Considerations

- Principle of Least Privilege
- EC2 instances are not publicly accessible
- SSH restricted to a single trusted IP
- Security Group referencing used instead of CIDR for internal communication
- Infrastructure managed through Terraform

---

# Cost Considerations

Resources used:

- t2.micro EC2 instances (AWS Free Tier eligible)
- Application Load Balancer
- Auto Scaling Group
- Default VPC
- Security Groups

To avoid unnecessary charges:

```bash
terraform destroy
```

after completing the project.

---

# Key Terraform Concepts Demonstrated

- Infrastructure as Code (IaC)
- Resources
- Data Sources
- Variables
- Outputs
- Launch Templates
- User Data
- Auto Scaling
- Application Load Balancer
- Security Groups
- Resource References
- Implicit Dependencies

---

# Lessons Learned

Through this project I learned:

- How to provision AWS infrastructure using Terraform
- The difference between resources and data sources
- How Launch Templates work with Auto Scaling Groups
- Why Target Groups perform health checks
- How Application Load Balancers distribute traffic
- How Terraform automatically manages dependencies between resources
- Infrastructure design for high availability

---

# Future Improvements

Potential enhancements include:

- HTTPS using AWS Certificate Manager
- Route 53 custom domain integration
- Remote Terraform state using Amazon S3
- DynamoDB state locking
- CloudWatch monitoring and alarms
- AWS WAF integration
- CI/CD deployment with GitHub Actions

---

# Author

**C.M.D**

Cloud & DevOps Engineer

Focused on building secure, scalable, and production-ready cloud infrastructure using AWS and Terraform.