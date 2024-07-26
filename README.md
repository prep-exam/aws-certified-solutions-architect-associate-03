# AWS Certified Solutions Architect - Associate (SAA-C03) Exam Topics

This document provides an overview of the AWS Certified Solutions Architect - Associate (SAA-C03) exam topics. Each section contains links to relevant topics for easier navigation, along with estimated coverage percentages to help prioritize your study efforts.

## Table of Contents

1. [AWS Core Services (40-45%)](#aws-core-services)
   - [Compute](#compute)
   - [Storage](#storage)
   - [Database](#database)
   - [Networking](#networking)
2. [Security and Compliance (25-30%)](#security-and-compliance)
   - [Identity and Access Management (IAM)](#identity-and-access-management-iam)
   - [Key Management Service (KMS)](#key-management-service-kms)
   - [Security Best Practices](#security-best-practices)
3. [Architectural Design (25-30%)](#architectural-design)
   - [High Availability and Disaster Recovery](#high-availability-and-disaster-recovery)
   - [Scalability and Elasticity](#scalability-and-elasticity)
   - [Performance Optimization](#performance-optimization)
4. [Deployment and Provisioning (5-10%)](#deployment-and-provisioning)
   - [Infrastructure as Code (IaC)](#infrastructure-as-code-iac)
   - [Deployment Strategies](#deployment-strategies)
5. [Monitoring and Reporting (5-10%)](#monitoring-and-reporting)
   - [CloudWatch](#cloudwatch)
   - [CloudTrail](#cloudtrail)
6. [Pricing and Support (5-10%)](#pricing-and-support)
   - [Cost Management](#cost-management)
   - [Support Plans](#support-plans)

## AWS Core Services (40-45%)

### Compute
- [EC2 (Elastic Compute Cloud)](##compute-ec2)
- [Lambda](##compute-lambda)
- [Elastic Beanstalk](##compute-elastic-beanstalk)
- [ECS (Elastic Container Service)](##compute-ecs)
- [EKS (Elastic Kubernetes Service)](##compute-eks)

### Storage
- [S3 (Simple Storage Service)](##storage-s3)
- [EBS (Elastic Block Store)](##storage-ebs)
- [EFS (Elastic File System)](##storage-efs)
- [Glacier](##storage-glacier)

### Database
- [RDS (Relational Database Service)](##database-rds)
- [DynamoDB](##database-dynamodb)
- [Redshift](##database-redshift)
- [Aurora](##database-aurora)

### Networking
- [VPC (Virtual Private Cloud)](##networking-vpc)
- [Route 53](##networking-route-53)
- [CloudFront](##networking-cloudfront)
- [Direct Connect](##networking-direct-connect)

## Security and Compliance (25-30%)

### Identity and Access Management (IAM)
- [Users and Groups](##identity-and-access-management-iam-users-and-groups)
- [Roles](##identity-and-access-management-iam-roles)
- [Policies](##identity-and-access-management-iam-policies)
- [Federation](##identity-and-access-management-iam-federation)

### Key Management Service (KMS)

#### Overview
- **AWS Key Management Service (KMS)** is a centralized service to create, manage, and rotate customer master keys (CMKs) used for encryption at rest.
- **Purpose**: Simplifies key management and integrates with other AWS services to enhance data security.

#### Key Types
- **Symmetric CMKs**: Uses a single key for both encryption and decryption operations.
- **Asymmetric CMKs**: Uses a public/private key pair. The public key is used for encryption or signature verification, while the private key is used for decryption or signature creation.

#### Key Rotation
- **Automatic Rotation**: CMKs can be configured to automatically rotate once per year.
- **Old Key Versions**: KMS retains older key versions to decrypt data encrypted with previous keys.

#### Key Management
- **Creation**: CMKs can be created via the AWS Management Console, CLI, or API.
- **Key Policies**: Define who can manage or use CMKs. Policies are attached directly to the CMK.
- **Grants**: Provide temporary access to CMKs for specific actions.
- **Aliases**: User-friendly names for CMKs. They make it easier to reference keys.

#### Encryption and Decryption
- **Direct Encryption**: KMS can encrypt small amounts of data directly.
- **Envelope Encryption**: Encrypts large datasets by using a data encryption key (DEK) to encrypt the data and then encrypts the DEK with a CMK.

#### Integration with Other AWS Services
- **S3**: Encrypts objects in S3 buckets.
- **EBS**: Encrypts EBS volumes to protect data at rest.
- **RDS**: Encrypts RDS databases and snapshots.
- **Lambda**: Securely access CMKs from Lambda functions.

#### Best Practices
- **Enable Key Rotation**: Regularly rotate keys to enhance security.
- **Least Privilege Access**: Use IAM policies and key policies to enforce the principle of least privilege.
- **Logging and Monitoring**: Use AWS CloudTrail to log and monitor KMS operations.


### Security Best Practices
- [Data Encryption](##security-best-practices-data-encryption)
- [Network Security](##security-best-practices-network-security)
- [IAM Best Practices](##security-best-practices-iam)

## Architectural Design (25-30%)

### High Availability and Disaster Recovery
- [Designing for Fault Tolerance](##high-availability-and-disaster-recovery-designing-for-fault-tolerance)
- [Backup and Restore](##high-availability-and-disaster-recovery-backup-and-restore)
- [Multi-Region Architectures](##high-availability-and-disaster-recovery-multi-region-architectures)

### Scalability and Elasticity
- [Auto Scaling](##scalability-and-elasticity-auto-scaling)
- [Load Balancers](##scalability-and-elasticity-load-balancers)
- [Database Scaling](##scalability-and-elasticity-database-scaling)

### Performance Optimization
- [Caching Strategies](##performance-optimization-caching-strategies)
- [Content Delivery](##performance-optimization-content-delivery)
- [Resource Optimization](##performance-optimization-resource-optimization)

## Deployment and Provisioning (5-10%)

### Infrastructure as Code (IaC)
- [CloudFormation](##infrastructure-as-code-iac-cloudformation)
- [Terraform](##infrastructure-as-code-iac-terraform)

### Deployment Strategies
- [Blue/Green Deployment](##deployment-strategies-blue-green-deployment)
- [Canary Deployment](##deployment-strategies-canary-deployment)
- [Rolling Updates](##deployment-strategies-rolling-updates)

## Monitoring and Reporting (5-10%)

### CloudWatch
- [Metrics and Alarms](##cloudwatch-metrics-and-alarms)
- [Logs](##cloudwatch-logs)
- [Dashboards](##cloudwatch-dashboards)

### CloudTrail
- [Event Logging](##cloudtrail-event-logging)
- [Insights](##cloudtrail-insights)

## Pricing and Support (5-10%)

### Cost Management
- [Cost Explorer](##cost-management-cost-explorer)
- [Budgets](##cost-management-budgets)
- [Savings Plans](##cost-management-savings-plans)

### Support Plans
- [Basic Support](##support-plans-basic-support)
- [Developer Support](##support-plans-developer-support)
- [Business Support](##support-plans-business-support)
- [Enterprise Support](##support-plans-enterprise-support)

---

 

### Notes
- The percentages listed are approximate and represent the weight of each domain in the exam.
- This document is a high-level overview of the exam topics. For detailed study, refer to AWS documentation and resources.
- Keep your AWS skills up to date with hands-on practice and exam readiness materials.
