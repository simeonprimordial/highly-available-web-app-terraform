# Architecture

## Overview

This project provisions a highly available web application on AWS using Terraform. The infrastructure is designed to improve application availability, distribute incoming traffic across multiple EC2 instances, and automatically recover from instance failures.

---

## Architecture Diagram

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

---

## Components

### Default VPC

The project uses the existing AWS Default VPC instead of provisioning a custom VPC. Terraform retrieves the VPC information using a data source, reducing deployment complexity while focusing on compute and load balancing.

---

### Default Subnets

The Application Load Balancer and Auto Scaling Group are deployed across the default subnets in multiple Availability Zones to provide high availability.

---

### Security Groups

Two Security Groups are implemented following the Principle of Least Privilege.

#### ALB Security Group

- Allows HTTP (Port 80) from the Internet
- Allows outbound traffic

#### EC2 Security Group

- Allows HTTP traffic only from the ALB Security Group
- Allows SSH only from the administrator's public IP
- Allows outbound traffic

This prevents direct Internet access to the EC2 instances.

---

### Launch Template

The Launch Template defines the standard configuration for every EC2 instance, including:

- Amazon Linux 2023 AMI
- Instance Type
- Security Group
- Key Pair
- User Data
- Tags

The Auto Scaling Group uses this template whenever a new instance must be launched.

---

### User Data

The EC2 instances automatically install and configure Apache during launch using a User Data script.

The script performs the following tasks:

- Updates system packages
- Installs Apache HTTP Server
- Enables the Apache service
- Starts the Apache service
- Creates a sample web page

---

### Application Load Balancer

The Application Load Balancer receives incoming HTTP requests and distributes traffic across healthy EC2 instances.

Responsibilities include:

- Request routing
- Health checks
- High availability
- Traffic distribution

---

### Target Group

The Target Group maintains a list of registered EC2 instances.

It periodically performs health checks and ensures that traffic is only routed to healthy instances.

---

### Auto Scaling Group

The Auto Scaling Group ensures that the required number of EC2 instances are always available.

Responsibilities include:

- Launching new EC2 instances
- Replacing unhealthy instances
- Maintaining desired capacity
- Scaling based on CPU utilization

---

## Terraform Design Decisions

### Data Sources

The following AWS resources are discovered rather than created:

- Default VPC
- Default Subnets
- Latest Amazon Linux 2023 AMI

This improves portability and reduces hardcoded values.

---

### Variables

Configuration values such as:

- AWS Region
- Instance Type
- Project Name
- Desired Capacity

are stored as variables to improve maintainability.

---

### Resource References

Terraform resource references are used instead of hardcoded IDs.

Example:

```hcl
aws_security_group.alb_sg.id
```

This allows Terraform to automatically manage dependencies between resources.

---

## High Availability

High availability is achieved through:

- Multiple Availability Zones
- Application Load Balancer
- Target Group Health Checks
- Auto Scaling Group
- Automatic Instance Replacement

The application remains accessible even if an EC2 instance fails.

---

## Benefits

- Infrastructure as Code
- Consistent deployments
- Automated recovery
- High availability
- Easier maintenance
- Version-controlled infrastructure