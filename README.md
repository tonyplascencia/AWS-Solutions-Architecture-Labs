# AWS Solutions Architecture Labs - Tony Plascencia

This repository contains technical documentation and implementation evidence of secure architectures on Amazon Web Services (AWS), following the **Well-Architected Framework**.

## Project 1: Identity Hardening & Governance
Implementation of a "Least Privilege" security scheme to protect critical infrastructure.

### Security Implementations:
- **Root Account Protection**: Delegated operations to an `admin` user, securing the Root account with physical MFA.
- **Hardware MFA**: Linked **YubiKey (FIDO2)** as a mandatory authentication factor.

### Preventive Policy: `IAM-Policy-Prevent-Accidental-Deletion`
This JSON policy applies an **Explicit Deny** to prevent any user from accidentally deleting critical resources without an active MFA session.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Deny",
            "Action": [
                "s3:DeleteBucket",
                "rds:DeleteDBInstance",
                "ec2:TerminateInstances",
                "dynamodb:DeleteTable"
            ],
            "Resource": "*",
            "Condition": {
                "BoolIfExists": {
                    "aws:MultiFactorAuthPresent": "false"
                }
            }
        }
    ]
}
```

Project 2: Team Management & Scalability (RBAC)
Role-Based Access Control (RBAC) design for development teams.

Key Implementations:
IAM Group: Devs group created with automatic permission inheritance for efficiency.

Access Control: Implementation of managed policies to allow EC2 and S3 development while restricting sensitive billing areas.

Financial Governance: AWS Budgets configuration with a $1.00 USD threshold and automated email alerts.

Real-Time Cost Monitoring
Demonstration of architectural efficiency and cost-conscious management.

Current Status: Optimized operation using the AWS Free Tier.

Monitored Expense: $0.03 USD (March 2026), proving effective resource cleanup and monitoring.

Credit Management: Strategic use of AWS credits to maintain a healthy project balance.

Professional Contact: tonyplascenciamzt@gmail.com
