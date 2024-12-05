# re:Invent 2024 - SEC324 - Pro Tip #1: Encryption at rest

![Secrets Manager](https://img.shields.io/badge/AWS-SecretsManager-orange)
![CloudFormation](https://img.shields.io/badge/CloudFormation-Templates-blue)
![AWS Security](https://img.shields.io/badge/AWS-Security-purple)
![License](https://img.shields.io/badge/License-MIT-green)

## Overview

This CloudFormation template demonstrates encryption at rest of secrets.
The passwords are generated in AWS Secrets Manager with specific character exclusions for enhanced compatibility and security.

## Parameters

### ParamExcludeCharacters
- **Type**: String
- **Default**: `\"@\ `
- **Purpose**: Defines characters to exclude from generated passwords
- **Use Case**: Ensures generated passwords are compatible with various systems and applications

## Features

### Encryption at rest
- Secrets are encrypted at rest in AWS Secrets Manager
- Secrets can be encrypted using AWS managed key
- Secrets can be encrypted using KMS Customer managed keys that providde more controls over the secrets and allow cross-account access.

### Password Generation
- Excludes problematic special characters
- Maintains password complexity
- Ensures system compatibility
- Follows security best practices

### Character Exclusion Benefits
- Prevents escape sequence issues
- Avoids shell interpretation problems
- Reduces application compatibility issues
- Maintains password strength while improving usability

## Security Considerations

- Password complexity is maintained despite character exclusions
- Minimum length requirements are enforced
- Random generation ensures unpredictability
- Compliant with security standards

## Usage Notes

- The excluded characters help prevent:
  - Command injection vulnerabilities
  - String parsing errors
  - Shell interpretation issues
  - Application compatibility problems

## Best Practices

- Review excluded characters for your specific use case
- Maintain minimum password length requirements
- Ensure sufficient character set diversity
- Test password compatibility with target systems

## Implementation Details

- Uses AWS Secrets Manager native password generation
- Implements secure random generation
- Maintains audit trail of password changes
- Supports automatic rotation

## Related Resources

- AWS Secrets Manager
- Password Policies
- Security Best Practices
- Compliance Requirements

---

*Created for re:Invent 2024 - SEC324 -  Code Talk*
