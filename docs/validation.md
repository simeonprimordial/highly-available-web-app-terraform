# Validation

## Objective

The objective of the validation process is to verify that the deployed infrastructure functions as expected and satisfies the project's high availability requirements.

---

## Validation Checklist

| Component | Validation | Status |
|-----------|------------|--------|
| Terraform Initialization | `terraform init` completed successfully | ✅ |
| Terraform Validation | `terraform validate` completed successfully | ✅ |
| Terraform Plan | Infrastructure changes reviewed | ✅ |
| Terraform Apply | Infrastructure deployed successfully | ✅ |
| Application Load Balancer | Created successfully | ✅ |
| Target Group | Healthy targets registered | ✅ |
| Launch Template | Created successfully | ✅ |
| Auto Scaling Group | Desired capacity maintained | ✅ |
| EC2 Instances | Apache installed automatically | ✅ |
| Website | Accessible through ALB DNS | ✅ |

---

## Validation Steps

### 1. Terraform Validation

Run:

```bash
terraform validate
```

Expected Result:

```
Success! The configuration is valid.
```

---

### 2. Terraform Plan

Run:

```bash
terraform plan
```

Expected Result:

Terraform displays the resources that will be created without making any changes.

---

### 3. Infrastructure Deployment

Run:

```bash
terraform apply
```

Expected Result:

Terraform provisions all AWS resources successfully.

---

### 4. Verify Auto Scaling Group

Navigate to:

```
AWS Console
→ EC2
→ Auto Scaling Groups
```

Confirm:

- Desired Capacity is met.
- Required number of EC2 instances are running.
- Instances are healthy.

---

### 5. Verify Target Group

Navigate to:

```
EC2
→ Target Groups
```

Confirm:

- Registered targets are healthy.
- Health checks are passing.

---

### 6. Verify Application Load Balancer

Navigate to:

```
EC2
→ Load Balancers
```

Copy the DNS name and open it in a web browser.

Expected Result:

The Apache web page loads successfully.

---

### 7. Test High Availability

Terminate one EC2 instance from the AWS Console.

Expected Result:

- Target Group marks the instance as unhealthy.
- Auto Scaling Group launches a replacement instance.
- New instance passes health checks.
- Website remains accessible.

---

## Validation Results

The deployment successfully demonstrated:

- Infrastructure created with Terraform
- High availability across multiple Availability Zones
- Automatic health monitoring
- Automatic instance replacement
- Successful traffic distribution using the Application Load Balancer