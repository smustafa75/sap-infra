# SAP Infrastructure on AWS

Terraform code for SAP infrastructure on AWS including HANA databases and supporting components.

## Architecture
- **Network**: VPC with public/private subnets, route tables, gateways, S3 endpoint
- **Compute**: 
  - 2 HANA DB servers with multiple EBS volumes
  - Bastion host, SAP Router
  - Optional SAP application server
- **Security**: Security groups for public/private resources
- **Monitoring**: CloudWatch alarms for HANA servers
- **IAM**: Instance profiles and roles

## Key Components
- **HANA Servers**: Configured with root, SAP, shared, data, and log volumes
- **Network**: VPC with DNS support, multi-AZ subnets, NAT gateway
- **Monitoring**: CPU (80%), disk (60%), memory (60%) alarms

## Important Notes
- **Cost Impact**: Significant AWS costs - review TFVARS carefully
- **Resources**: ~49 resources, exceeds AWS free tier
- **AWS Profile**: Uses "render" profile by default
- **Prerequisites**: AWS account, CLI with "render" profile, "bastion_pair_01" SSH key

## Terraform Version
```
Terraform v1.1.2
+ provider registry.terraform.io/hashicorp/aws v3.71.0
+ provider registry.terraform.io/hashicorp/random v3.1.0
+ provider registry.terraform.io/hashicorp/template v2.2.0
```
