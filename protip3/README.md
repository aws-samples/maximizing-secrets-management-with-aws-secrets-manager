# re:Invent 2024 - SEC324 - ProTip #3 - Secrets consumption using Secrets Manager agent
![Secrets Manager](https://img.shields.io/badge/AWS-SecretsManager-orange)
![CloudFormation](https://img.shields.io/badge/CloudFormation-Templates-blue)
![AWS Security](https://img.shields.io/badge/AWS-Security-purple)
![License](https://img.shields.io/badge/License-MIT-green)


This CloudFormation template sets up the necessary infrastructure prerequisites for an AWS environment with secure access patterns to demonstrate how AWS Secrets Manager agent can work.

## Overview

This template creates:
- A new VPC with public and private subnets
- Security Groups
- NAT Gateway and Internet Gateway for package downloads
- EC2 instance configured with AWS Systems Manager Session Manager access
- VPC Flow Logs with CloudWatch integration
- Required IAM roles and policies
- RDS instance with master credentials automatically managed by AWS Secrets Manager.

## Prerequisites

- An AWS account
- Appropriate permissions to create the resources defined in the template
- AWS CLI configured (if deploying via CLI)

## Parameters

The template accepts the following parameters:

- **ParamProjectName**: Project name identifier (Default: "reinv2024-sec324-protip3")
- **ParamVPCCidr**: CIDR block for the VPC (Default: 10.20.40.0/24)
- **ParamRssEC2SubnetACidr**: CIDR for Private Subnet A (Default: 10.20.40.0/26)
- **ParamSubnetBCidr**: CIDR for Private Subnet B (Default: 10.20.40.64/26)
- **ParamSubnetCCidr**: CIDR for Public Subnet C (Default: 10.20.40.128/26)
- **ParamLatestAmiId**: Latest Amazon Linux 2 AMI ID (auto-retrieved from SSM Parameter Store)
- **DBPort**: Database port number (Default: 3306)
- **ParamDBName**: Database name (Default: 'Campaign')
- **DBInstanceClass**: Database instance type (Default: 'db.t3.micro')
- **DBUsername**: Username for database access

## Resources Created

1. **VPC Infrastructure**
   - VPC with DNS support enabled
   - 2 Private Subnets (A and B)
   - 1 Public Subnet (C) that will host a NAT Gateway
   - Internet Gateway
   - VPC Flow Logs

2. **Security**
   - IAM roles for EC2 and Systems Manager integration
   - Security Groups
   - VPC Flow Logs with CloudWatch integration

3. **Compute**
   - EC2 instance with Systems Manager Session Manager access
   - Instance Profile with necessary permissions

4. **Database**
   - RDS DB MySQL instance in private subnet
   - RDS master credentials managed by AWS Secrets Manager

## Security Features

- Systems Manager Session Manager for secure instance access (no SSH required)
- VPC Flow Logs for network traffic monitoring
- Managed IAM policies with least privilege access
- Secure secrets management integration

## Testing
Please follow the [official documentation](https://docs.aws.amazon.com/secretsmanager/latest/userguide/secrets-manager-agent.html) and this [blog post](https://aws.amazon.com/blogs/security/how-to-use-the-aws-secrets-manager-agent/) to install AWS Secrets Manager agent.

### Agent installation
Connect to your private EC2 instance using Session Manager.
Once connected, you can run the command below in your EC2 instance to download, build, install the agent and configure the permission on the access token.

   ```bash
      cd ~;git clone https://github.com/aws/aws-secretsmanager-agent
      sudo yum -y groupinstall "Development Tools"
      date
      curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
      . "$HOME/.cargo/env"
      cd aws-secretsmanager-agent
      pwd;date;
      cargo build --release
      cd aws_secretsmanager_agent/configuration
      sudo ./install
      pwd;date
      sudo cp /var/run/awssmatoken /tmp
      sudo chown ssm-user /tmp/awssmatoken
      whoami
      pwd
      date
   ```

### Use the agent to get the DB credentials
Human are kept away from secrets; therefore programatically use the agent to obtain the secret value to connect to the DB. Please find the name of secret created for the DB instance deployed.

   ```bash
   echo 'now let's work with DB secret to connect to it ;-)'
   region='<YOUR-REGION>'
   aws secretsmanager list-secrets --region $region
   secret='<DB_MASTER_USER_SECRET_NAME>'
   aws secretsmanager describe-secret --secret-id $secret --region $region
   echo 'The secret ARN is:'
   curl -H "X-Aws-Parameters-Secrets-Token: $(</tmp/awssmatoken)" localhost:2773/secretsmanager/get?secretId=$secret | jq -r .ARN
   echo 'The DB username is :'
   username=`curl -H "X-Aws-Parameters-Secrets-Token: $(</tmp/awssmatoken)" localhost:2773/secretsmanager/get?secretId=$secret | jq -r .SecretString | jq -r .username`
   password=`curl -H "X-Aws-Parameters-Secrets-Token: $(</tmp/awssmatoken)" localhost:2773/secretsmanager/get?secretId=$secret | jq -r .SecretString | jq -r .password`
   echo $username
   ```
### Connect to the DB created using the credentials stored in AWS Secrets Manager
Get the database endpoint name of the database created with this template, and set its value below.
**Note:** To connect to the MySQL database, you need the username and password defined previously.

   ```
   dbendpoint='<DATABASE_NAME>.ABCD124563ED.<REGION>.rds.amazonaws.com'
   echo 'Now connect to the database without seeing the secret value...'
   mysql -h $dbendpoint -P 3306 -u $username -p$password

   ```

## Notes

- You don't need to see the secrets, your application relies on AWS Secrets Manager agent to get the needed secrets
- The EC2 instance is accessible via AWS Systems Manager Session Manager only
- Database credentials should be managed securely through AWS Secrets Manager



## EC2 Instance Configuration

The EC2 instance comes pre-configured with:
- AWS Systems Manager Agent
- MariaDB client
- Git
- AWS CloudFormation bootstrap tools
- JSON processing capabilities (`jq`)

## Best Practices Implemented

- Use the Secrets Manager agent instead of direct API call
- Keep humans away from secrets
- Private hosting of sensitive resources
- Use AWS Systems Manager Session Manager instead of opening SSH port over internet
- VPC Flow Logs for network monitoring
- Proper subnet segregation (public/private).

## Deployment

The template can be deployed through:
- AWS Management Console
- AWS CLI
- AWS CloudFormation API



*Created for re:Invent 2024 - SEC324 - Code Talk*