# Cleanup

## Objective

To prevent unnecessary AWS charges by removing all provisioned resources.

---

## Destroy Infrastructure

Navigate to the Terraform directory.

Run:

```bash
terraform destroy
```

Terraform displays all resources scheduled for deletion.

Type:

```
yes
```

Terraform removes:

- Auto Scaling Group
- Launch Template
- Application Load Balancer
- Target Group
- Security Groups

---

## Verify Resource Deletion

Confirm the following resources no longer exist:

- EC2 Instances
- Auto Scaling Group
- Application Load Balancer
- Target Group
- Security Groups

---

## Verify Billing

Open:

```
AWS Billing Console
```

Confirm that no billable resources remain.

---

## Local Cleanup

Optional:

Remove Terraform working files.

```bash
rm -rf .terraform
rm terraform.tfstate*
```

Do **not** delete:

- Terraform source files
- Documentation
- README
- Architecture diagrams

These should remain in the repository for future reference and version control.