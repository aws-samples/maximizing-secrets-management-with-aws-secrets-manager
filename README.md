# 🔐 re:Invent 2024 - SEC324 - Maximizing secrets management with AWS Secrets Manager

![Secrets Manager](https://img.shields.io/badge/AWS-SecretsManager-orange)
![CloudFormation](https://img.shields.io/badge/CloudFormation-Templates-blue)
![AWS Security](https://img.shields.io/badge/AWS-Security-purple)
![IAM](https://img.shields.io/badge/AWS-IAM-yellow)
![License](https://img.shields.io/badge/License-MIT-green)


This is the repository for the re:Invent 2024 Code Talk session SEC-324 "Maximizing your secrets management". It is a collection of AWS CloudFormation templates demonstrating security best practices and patterns for AWS infrastructure. Each template is carefully crafted to showcase specific security implementations and guidelines.

This repository structure follows the protips that are shared during the session.

## Disclaimer
This collection of CloudFormation templates are for demonstration purpose and are not production ready.
Remember to delete the deployed stack if you are not using it anymore.
The code is scanned with `cfn-nag` and the resulting security findings are available with template file.

## 📑 Templates Overview

<details>
<summary><b>🌐 Pro Tip #1: Encryption at rest </b></summary>

### `protip1.yaml`
- ✨ Secrets encryption at rest
- 🗝️ AWS KMS implementation
- 📝 Usagge of AWS managed keys vs Customer managed keys
- 🔒 Ramdomly generated password with Secrets Manager
</details>

<details>
<summary><b>👤 Pro Tip #2: IAM and Access Management</b></summary>

### `protip2.yaml`
- 🔑 Access controls on secrets
- 👥 Role-based access control
- ⚙️ Attribute-based Access control
- 🎯 Least privilege permissions
- 📋 Resource-based policies
</details>

<details>
<summary><b>💻 Pro Tip #3: Consume secrets with AWS Secrets Manager agent</b></summary>

### `protip3.yaml`
- 🔒 Private EC2 instance access pattern and package installation
- ⚡ Systems Manager Session Manager configuration
- 🗄️ Secure database connectivity - private database
- 🔌 Testing connectivity between the agent and AWS Secrets Mananger
- 📊 Connectivity to the database
</details>

<details>
<summary><b>🔐 Pro Tip #4: Secrets Rotation </b></summary>

### `protip4.yaml`
- 🗝️ Creation of DB user with secrets generated and stored by AWS Secrets Manager
- 🔒 Attachment of the secret to a DB user
- 🔄 Creation of rotation pattern
- 💾 Encrypted storage solutions
</details>

<details>
<summary><b>🤫 Pro Tip #5: Disaster recover and secrets replication</b></summary>

### `protip5.yaml`
- 🔑 AWS Secrets Manager replication
- 🔄 Secrets Region replication
- 🛡️ Encryption for secrets
</details>

<details>
<summary><b>📋 Pro Tip #6: Compliance and Incident Response</b></summary>

### `protip6.yaml`
- ✅ AWS Config compliance monitoring
- ⚡ EventBridge rules for notifications
- 📢 SNS topics for alerts
- 🚨 Incident response patterns
- 👮 Secrets compliance monitoring
</details>

## 🌟 Common Features

- 📝 Infrastructure as Code (IaC) best practices
- 🛡️ Secure resource configurations
- 🎯 Least privilege access controls
- 🤖 Automated security controls

## 📋 Prerequisites

- ☁️ AWS Account with appropriate permissions
- 📘 Understanding of AWS CloudFormation
- 🔒 Basic knowledge of AWS security services
- 💻 AWS CLI configured (for command-line deployment)

## 🛡️ Security Best Practices

### 🌐 Network Security
- Subnet segregation
- Security group configurations
- Network ACL implementation
- VPC Flow Logs

### 👤 Access Management
- IAM roles and policies
- Resource-based policies
- Service-linked roles
- Least privilege access

### 🔐 Encryption
- KMS key management
- Resource encryption
- Secure key rotation
- Transport encryption

### 📊 Monitoring and Logging
- CloudWatch integration
- AWS Config rules
- VPC Flow Logs
- Access logging

### ✅ Compliance
- Automated compliance checking
- Regular monitoring
- Incident response
- Audit trails

## 📚 Usage Guidelines

1. 📖 Review each template's specific README
2. 🚀 Deploy using AWS CloudFormation
3. 📊 Monitor through CloudWatch
4. 🔍 Review security findings
5. 🔄 Maintain and update regularly

## 🔧 Maintenance

- 📋 Regular security configuration reviews
- 🔄 Updates for new best practices
- 👀 Security findings monitoring
- 🔑 Rotation of secrets and keys
- 📊 Access pattern reviews

## ⚠️ Security Considerations

- 🛡️ AWS security best practices implementation
- 🔄 Regular security patch updates
- 📊 AWS Security Hub monitoring
- 📝 Access logs review
- ✅ Compliance maintenance

## 📝 Notes

- 🎓 Templates for demonstration and learning
- ⚙️ Modify parameters as needed
- 🔒 Follow AWS security best practices
- 🔄 Keep configurations updated
- 📢 Monitor security announcements

---

## 📜 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

*Made with ❤️ for AWS Security*
