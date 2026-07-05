# Security

## Security Overview

Security was implemented using AWS Security Groups and the Principle of Least Privilege.

Each AWS resource is granted only the permissions required to perform its function.

---

# Security Architecture

```
Internet
    │
HTTP (80)
    │
    ▼
Application Load Balancer
    │
HTTP (80)
    │
    ▼
EC2 Instances
```

The EC2 instances are never directly exposed to the Internet.

---

## Application Load Balancer Security Group

### Inbound Rules

| Protocol | Port | Source |
|----------|------|--------|
| TCP | 80 | 0.0.0.0/0 |

Purpose:

Allow HTTP requests from users.

---

### Outbound Rules

Allow all outbound traffic.

This enables communication with the EC2 instances.

---

## EC2 Security Group

### Inbound Rules

| Protocol | Port | Source |
|----------|------|--------|
| TCP | 80 | ALB Security Group |
| TCP | 22 | Administrator Public IP |

Purpose:

- HTTP traffic only from the ALB.
- SSH restricted to the administrator.

---

### Outbound Rules

Allow all outbound traffic.

---

## Security Best Practices

The project implements the following AWS security best practices:

- Principle of Least Privilege
- Security Group referencing
- Restricted SSH access
- Infrastructure as Code
- Automatic instance replacement
- No direct public access to EC2 instances

---

## Future Security Improvements

Future enhancements may include:

- HTTPS using AWS Certificate Manager
- AWS WAF
- AWS Shield
- IAM Roles for EC2
- AWS Systems Manager Session Manager
- AWS Secrets Manager