# Troubleshooting

## Terraform Validation Errors

### Problem

Terraform validation fails.

### Solution

Run:

```bash
terraform fmt
terraform validate
```

Review the reported syntax errors.

---

## Provider Download Failure

### Problem

`terraform init` fails.

### Solution

- Check Internet connectivity.
- Verify Terraform installation.
- Retry `terraform init`.

---

## Website Not Loading

### Possible Causes

- Apache not running.
- Target Group unhealthy.
- Security Group misconfiguration.

### Resolution

Verify:

- Apache service
- EC2 Security Group
- ALB Security Group
- Target Group health checks

---

## Unhealthy Targets

### Causes

- User Data failed.
- Apache failed to install.
- Wrong health check path.

### Resolution

Inspect:

- EC2 System Logs
- Cloud-Init logs
- Apache service status

---

## Auto Scaling Not Replacing Instances

Verify:

- Desired Capacity
- Health Check Type
- Launch Template configuration

---

## SSH Connection Failure

Verify:

- Correct key pair
- Public IP allowed
- EC2 instance running
- Security Group rules