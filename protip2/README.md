# re:Invent 2024 - SEC324 - Pro Tip #2: Secrets Access Control Patterns

![Secrets Manager](https://img.shields.io/badge/AWS-SecretsManager-orange)
![CloudFormation](https://img.shields.io/badge/CloudFormation-Templates-blue)
![AWS Security](https://img.shields.io/badge/AWS-Security-purple)
![IAM](https://img.shields.io/badge/AWS-IAM-yellow)
![License](https://img.shields.io/badge/License-MIT-green)

## Overview

This CloudFormation template demonstrates different access control patterns in AWS Secrets Manager:
- Role-Based Access Control (RBAC)
- Resource-Based Policies
- Attribute-Based Access Control (ABAC)

## 🎯 Resources created

### Secrets
- **SecretProTip2B**
  - Basic secret with KMS encryption
  - Used to demonstrate RBAC and ABAC
  - Tagged with different project name for ABAC testing

- **SecretProTip2C**
  - Secret with resource-based policy
  - Demonstrates tag protection
  - Configured with specific ABAC permissions

### IAM Roles

#### IAMRoleTestABAC
- Demonstrates ABAC implementation
- Can only access secrets with matching project tags
- List capability for all secrets
- Restricted from modifying tags on protected secrets

#### IAMRoleListSecrets
- Demonstrates RBAC implementation
- Can list and describe secrets
- Cannot retrieve secret values
- Full CloudShell access for testing

## 📋 Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| ParamProjectName | r24-sec324-protip2 | Project identifier |
| ParamPrefix | SEC324-ProTip2- | Prefix for resource names |
| ParamPasswordLength | 12 | Minimum password length |
| ParamUsername | r24-sec324-protip2-username | Default username |
| ParamExcludeCharacters | \"@\\ | Characters to exclude from secrets |

## 🔒 Security Features

### RBAC Implementation
- Separate roles for different access levels
- Clear separation of duties
- Principle of least privilege

### ABAC Controls
- Tag-based access control
- Project-based restrictions
- Dynamic permission evaluation

### Resource-Based Policies
- Protection of resource tags
- Explicit deny statements
- Fine-grained access control

## 🛠️ Usage Examples

### Testing RBAC
- Assume the IAMRoleListSecrets role (you can use the AWS console)
- You should be able to:
    - List all secrets
    - Describe secrets
    - View resource policies

- You should **NOT** be able to:
  -  Retrieve ANY secret values


## Implementation Notes
- ABAC requires proper tag management
- Resource policies protect critical tags
- RBAC provides baseline access control
- CloudShell access included for testing
- AWS CloudTrail records the call to AWS Secrets Manager

*Created for re:Invent 2024 - SEC324 - Code Talk*