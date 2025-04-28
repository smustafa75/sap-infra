# SAP Infrastructure on AWS

This repository contains Terraform code to set up a complete SAP infrastructure environment on AWS, including HANA databases, application servers, and supporting components.

## Architecture Overview

The infrastructure consists of the following components:

- **Network Layer**: VPC with public and private subnets, route tables, internet gateway, NAT gateway, and S3 VPC endpoint
- **Compute Layer**: 
  - 2 HANA database servers (primary and secondary) with multiple EBS volumes
  - Bastion host for secure access to private resources
  - SAP Router server for SAP connectivity
  - (Optional/Commented out) SAP application server
- **Security Layer**: Security groups for public and private resources
- **Monitoring**: CloudWatch alarms for HANA servers (CPU, memory, disk utilization)
- **IAM**: Instance profiles and roles for EC2 instances

## Resource Details

### HANA Database Servers
- Two identical HANA DB instances with:
  - Root volume (gp3)
  - SAP volume (/dev/sdb)
  - Shared volume (/dev/sdc)
  - Data volume (/dev/sdd)
  - Log volume (/dev/sde)
- All volumes are configurable via variables

### Network Configuration
- VPC with DNS support enabled
- Public and private subnets across availability zones
- S3 VPC endpoint for private subnet access to S3
- NAT gateway for private subnet internet access

### Monitoring
- CloudWatch alarms for both HANA servers:
  - CPU utilization (threshold: 80%)
  - Disk utilization (threshold: 60%)
  - Memory utilization (threshold: 60%)

## Important Notes

- **Cost Impact**: This infrastructure deploys multiple EC2 instances and EBS volumes that will incur significant AWS costs. Replace the TFVARS content carefully as it may have very high cost impact.
- **Resource Count**: The deployment creates approximately 49 resources and will exceed the AWS free tier limits.
- **Compute Configuration**: The compute module contains dynamic EBS volume configuration. Review it carefully before deployment.
- **AWS Profile**: The code is configured to use the "render" AWS profile. Update this if needed.

## Prerequisites

- AWS account with appropriate permissions
- AWS CLI configured with "render" profile
- SSH key pair named "bastion_pair_01" (referenced in the code)

## Terraform Version

```
Terraform v1.1.2
+ provider registry.terraform.io/hashicorp/aws v3.71.0
+ provider registry.terraform.io/hashicorp/random v3.1.0
+ provider registry.terraform.io/hashicorp/template v2.2.0
```

