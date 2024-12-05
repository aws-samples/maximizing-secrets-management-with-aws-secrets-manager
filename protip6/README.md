# re:Invent 2024 - SEC324 - Pro Tip #6: Compliance and Incident Response

![Secrets Manager](https://img.shields.io/badge/AWS-SecretsManager-orange)
![CloudFormation](https://img.shields.io/badge/CloudFormation-Templates-blue)
![AWS Security](https://img.shields.io/badge/AWS-Security-purple)
![License](https://img.shields.io/badge/License-MIT-green)

This CloudFormation template demonstrates how to implement compliance monitoring and incident response for AWS Secrets Manager using AWS Config rules, Amazon EventBridge for event detection and Amazon SNS for notification.

## Overview

This template sets up an automated compliance monitoring system that:
- Creates secrets with different encryption methods
- Monitors secrets compliance using AWS Config rule
- Reeact to secrets non compliance using Amazon EventBridge
- Sends notifications for non-compliant resources via SNS

## Prerequisites

- AWS Config must be enabled in the region where you deploy this template
- Appropriate IAM permissions to create and manage:
  - AWS Secrets Manager secrets
  - AWS KMS keys
  - AWS Config rules
  - EventBridge rules
  - SNS topic

## Components

### Secrets Management
- Creates two secrets in AWS Secrets Manager:
  - SecretA: Uses default AWS managed encryption
  - SecretB: Uses customer-managed KMS key encryption
- Automatically generates secure passwords with configurable length

### Encryption
- Creates customer-managed KMS keys for:
  - Secret encryption
  - SNS topic encryption
- Implements KMS key rotation policies
- Defines granular key usage permissions

### Monitoring and Compliance
- AWS Config rule to monitor secrets using customer-managed KMS keys
- EventBridge rule to capture non-compliant events
- SNS topic for compliance notifications

## Parameters

- **ParamProjectName**: Project identifier (Default: "r24-sec324-protip6")
- **ParamSubscription**: Notification endpoint (Default email address provided)
- **ParamExcludeCharacters**: Characters to exclude from generated passwords
- **ParamPasswordLength**: Minimum password length (Default: 20)
- **ParamSubscriptionProtocol**: Notification protocol (Options: http, https, email, email-json, sms, sqs, application, lambda)

## Security Features

- Automatic key rotation for KMS keys
- Encrypted SNS topics
- Least privilege access policies
- Compliance monitoring and alerting
- Secure password generation

## Outputs

The template provides the following outputs:
- Stack name
- Secret IDs for both created secrets
- SNS Topic ARN

## Best Practices Implemented

- Use of customer-managed KMS keys for enhanced control
- Automated compliance monitoring
- Secure notification handling
- Granular IAM permissions
- Automated incident response through EventBridge

## Compliance Monitoring

The template monitors:
- Use of customer-managed KMS keys for secrets
- Compliance status changes
- Non-compliant resource configurations

## Notifications

Non-compliance events trigger:
1. AWS Config detection
2. EventBridge rule evaluation
3. SNS notification to subscribed endpoints

## Security Considerations

- All sensitive data is encrypted at rest
- KMS keys have restricted usage policies
- SNS topics are encrypted
- EventBridge rules have specific targeting



*Created for re:Invent 2024 - SEC324 - Code Talk*