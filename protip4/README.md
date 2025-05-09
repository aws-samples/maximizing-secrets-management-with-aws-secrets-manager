# re:Invent 2024 - SEC324 - Pro Tip #4: Secrets Lifecycle

![Secrets Manager](https://img.shields.io/badge/AWS-SecretsManager-orange)
![CloudFormation](https://img.shields.io/badge/CloudFormation-Templates-blue)
![AWS Security](https://img.shields.io/badge/AWS-Security-purple)
![IAM](https://img.shields.io/badge/AWS-IAM-yellow)
![VPC](https://img.shields.io/badge/AWS-VPC-blue)
![RDS](https://img.shields.io/badge/AWS-RDS-red)
![License](https://img.shields.io/badge/License-MIT-green)


## Overview

This CloudFormation template sets up a secure network architecture with private subnets, VPC endpoints, and secure database access patterns using AWS Secrets Manager.

A secret will be created by AWS Secrets Manager and the password will be randomly generated. That secret will be use to configure a database user that the Lambda function will create.

That secret will be update in Secrets Manager to be attached to the neew database user and the database information. A rotation will be configured.

## Architecture Components

### VPC Configuration
- Custom VPC with DNS support
- Two private subnets across different AZs
- Secure network isolation
- CIDR: 10.20.30.40/24

### VPC Endpoints
- RDS VPC Endpoint
- Secrets Manager VPC Endpoint
- Private DNS enabled
- Interface endpoint type

### Security Groups
1. **RDS Security Group**
   - Inbound access from Lambda only
   - Restricted outbound to loopback
   - Port 3306 (MySQL)

2. **Lambda Security Group**
   - Outbound to RDS
   - Outbound to VPC endpoints
   - Restricted to necessary ports

3. **Endpoint Security Group**
   - HTTPS (443) access
   - Restricted outbound to loopback

## Database Configuration

### RDS Instance
- MySQL 8.0.33
- Private subnet placement
- Encrypted storage
- IAM database authentication
- Managed master user password

### Secrets Management
- Automated password generation
- Secure storage in AWS Secrets Manager
- Multiple user secrets (DBUserA, DBUserB)
- KMS encryption

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| VpcCIDR | 10.20.30.40/24 | VPC CIDR block |
| SubnetACIDR | 10.20.30.40/26 | Private Subnet A |
| SubnetBCIDR | 10.20.30.64/26 | Private Subnet B |
| DBName | Campain | Database name |
| DBInstanceClass | db.t3.micro | Database instance type |
| DBPort | 3306 | Database port |

## Security Features

### Network Security
- Private subnets only
- No Internet Gateway
- VPC Endpoints for AWS services
- Restricted security group rules

### Access Control
- IAM authentication
- Secrets Manager integration
- Least privilege permissions
- Security group isolation

### Encryption
- Storage encryption enabled
- In-transit encryption
- KMS key management
- Secure secret storage

## Lambda Integration

### Lambda Function
- VPC-enabled
- Private subnet placement
- Secure database access
- PyMySQL Layer support

### IAM Role
- VPC execution permissions
- Secrets Manager access
- Minimal required permissions
- Secure secret retrieval

## Best Practices Implemented

1. Network Isolation
   - Private subnets
   - No public access
   - Endpoint-based connectivity

2. Security Controls
   - Encrypted storage
   - IAM authentication
   - Secure secrets handling
   - Least privilege access

3. High Availability
   - Multi-AZ subnet design
   - Multiple VPC endpoints
   - Redundant configuration

## Maintenance Notes

- Review security group rules periodically
- Monitor VPC endpoint usage
- Audit database access patterns
- Update Lambda layers as needed

## Important Considerations

- All resources are deployed in private subnets
- Database is not publicly accessible
- Secrets are managed through AWS Secrets Manager
- Security groups follow least privilege principle

---

*Created for re:Invent 2024 SEC324 Code Talk*
