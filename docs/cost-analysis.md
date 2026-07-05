# Cost Analysis

## Objective

This project was designed to demonstrate a production-style highly available architecture while remaining cost-conscious for learning purposes.

---

## AWS Services Used

| Service | Purpose |
|----------|---------|
| EC2 | Web Servers |
| Application Load Balancer | Traffic Distribution |
| Auto Scaling | High Availability |
| Security Groups | Network Security |
| Launch Template | EC2 Configuration |
| VPC | Networking |

---

## Estimated Costs

Typical resources include:

- 2 × t2.micro EC2 Instances
- 1 Application Load Balancer
- Auto Scaling Group
- Default VPC
- Security Groups

The Application Load Balancer is the primary cost component because it is not covered by the AWS Free Tier.

---

## Cost Optimization

To reduce costs:

- Use t2.micro instances for lab environments.
- Destroy resources immediately after testing.
- Avoid unnecessary scaling.
- Monitor usage with AWS Cost Explorer.

---

## Cleanup

Destroy all resources using:

```bash
terraform destroy
```

This prevents ongoing AWS charges.