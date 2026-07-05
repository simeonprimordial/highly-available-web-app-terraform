# Deployment Guide

## Prerequisites

Before deployment, ensure the following tools are installed:

- Terraform
- AWS CLI
- Git
- Visual Studio Code (optional)

AWS credentials must be configured.

---

## Clone Repository

```bash
git clone https://github.com/<username>/highly-available-web-app-terraform.git

cd highly-available-web-app-terraform/terraform
```

---

## Configure Variables

Create a file named:

```
terraform.tfvars
```

Example:

```hcl
key_pair_name = "your-keypair-name"
```

---

## Initialize Terraform

```bash
terraform init
```

Terraform downloads the required AWS provider and initializes the working directory.

---

## Format Configuration

```bash
terraform fmt
```

Formats Terraform files according to HashiCorp standards.

---

## Validate Configuration

```bash
terraform validate
```

Checks the configuration for syntax and structural errors.

---

## Review Execution Plan

```bash
terraform plan
```

Displays the infrastructure changes Terraform will perform.

---

## Deploy Infrastructure

```bash
terraform apply
```

Type:

```
yes
```

to confirm deployment.

Terraform provisions all AWS resources.

---

## Verify Deployment

After deployment:

- Verify the Auto Scaling Group is healthy.
- Verify the Target Group shows healthy targets.
- Copy the ALB DNS name from the Terraform outputs.
- Open the DNS name in a web browser.
- Confirm the Apache web page loads successfully.

---

## Destroy Infrastructure

To avoid unnecessary AWS charges:

```bash
terraform destroy
```

Confirm by typing:

```
yes
```

Terraform removes all managed infrastructure.