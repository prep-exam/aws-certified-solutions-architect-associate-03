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
 
### Security Best Practices

#### Data Encryption
- **At Rest**:
  - **Amazon S3**: Use server-side encryption with S3-managed keys (SSE-S3), AWS Key Management Service (SSE-KMS), or a customer-provided key (SSE-C).
  - **Amazon EBS**: Enable encryption for EBS volumes using AWS KMS keys. Ensure that snapshots are encrypted as well.
  - **Amazon RDS**: Enable encryption for databases and backups using AWS KMS. Encrypt data at rest and in transit.
  - **Amazon Aurora**: Use encryption for Aurora clusters and snapshots. Encryption integrates with AWS KMS.
  - **AWS Glacier**: Encrypt archived data using server-side encryption with AWS KMS or S3-managed keys.

- **In Transit**:
  - **TLS/SSL**: Use TLS/SSL to secure data transmitted over networks. Ensure that services and applications use strong encryption protocols.
  - **AWS Certificate Manager (ACM)**: Manage SSL/TLS certificates for your applications using ACM to secure data in transit.

- **Key Management**:
  - **AWS KMS**: Utilize AWS KMS to manage encryption keys, implement key policies, and enable automatic key rotation.
  - **Custom Keys**: If using custom encryption solutions, ensure they adhere to security best practices and integrate with AWS services effectively.

#### Network Security
- **VPC Security**:
  - **Security Groups**: Configure security groups to control inbound and outbound traffic to EC2 instances. Use least privilege rules and regularly review group configurations.
  - **Network ACLs**: Use network ACLs to control traffic at the subnet level. Configure rules for both inbound and outbound traffic.
  - **VPC Peering**: Use VPC peering to securely connect VPCs within the same region or across regions. Ensure appropriate route tables and security group settings.

- **Private Connectivity**:
  - **AWS Direct Connect**: Use AWS Direct Connect for private, dedicated connections between your on-premises data center and AWS. This reduces exposure to the public internet and improves security.
  - **AWS PrivateLink**: Access AWS services and VPC endpoints privately using AWS PrivateLink, eliminating exposure to the public internet.

- **Network Monitoring**:
  - **VPC Flow Logs**: Enable VPC Flow Logs to capture detailed information about network traffic. Use these logs for monitoring and security analysis.
  - **AWS WAF**: Implement AWS Web Application Firewall (WAF) to protect your web applications from common web exploits.

- **DDoS Protection**:
  - **AWS Shield**: Use AWS Shield Standard for protection against DDoS attacks. AWS Shield Advanced provides additional protections and response capabilities.
  - **Amazon CloudFront**: Use CloudFront to distribute content and mitigate DDoS attacks by caching content at edge locations.

#### IAM Best Practices
- **Principle of Least Privilege**:
  - **Permissions**: Grant only the permissions necessary for users and roles to perform their required tasks. Regularly review and adjust permissions as needed.
  - **Roles**: Use IAM roles with appropriate permissions for services and applications instead of embedding credentials in applications.

- **User Management**:
  - **Groups**: Organize users into groups with shared permissions. This simplifies management and ensures consistent access controls.
  - **MFA**: Require Multi-Factor Authentication (MFA) for users, especially for privileged accounts. Enable MFA for AWS root accounts and sensitive operations.

- **Policies**:
  - **Managed Policies**: Use AWS managed policies for common tasks to reduce the risk of misconfiguration. Consider custom policies when fine-grained control is required.
  - **Policy Conditions**: Use IAM policy conditions to enforce rules, such as IP address restrictions or MFA requirements, for accessing resources.

- **Auditing and Monitoring**:
  - **CloudTrail**: Enable AWS CloudTrail to log and monitor API calls made within your AWS environment. Use CloudTrail logs to investigate and audit access and actions.
  - **IAM Access Analyzer**: Use IAM Access Analyzer to identify and review resources shared with external entities. Ensure that sharing is intentional and secure.

- **Secure Access**:
  - **Temporary Credentials**: Use AWS Security Token Service (STS) to generate temporary security credentials for short-term access. Avoid using long-term credentials wherever possible.
  - **Credential Rotation**: Regularly rotate credentials and secrets to minimize the risk of unauthorized access.



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

#### Metrics and Alarms
- **Metrics**:
  - **Standard Metrics**: AWS CloudWatch automatically collects metrics from AWS services (e.g., CPU utilization, disk I/O, network traffic). Each AWS service provides specific metrics that can be monitored.
  - **Custom Metrics**: You can publish custom metrics from your applications and services using the CloudWatch API. This allows you to monitor application-specific performance indicators.
  - **Namespace**: Metrics are organized into namespaces, which help to categorize them. Each service and custom metric uses a specific namespace.

- **Alarms**:
  - **Creation**: Set up alarms to monitor specific metrics and trigger actions based on thresholds (e.g., CPU utilization > 80%).
  - **Actions**: Configure alarms to send notifications (e.g., SNS notifications), execute Auto Scaling policies, or trigger Lambda functions.
  - **Types**: Alarms can be based on static thresholds or anomaly detection (CloudWatch Anomaly Detection) to identify unusual patterns in your metrics.
  - **State**: Alarms have three states: OK, ALARM, and INSUFFICIENT_DATA. Each state indicates the status of the monitored metric relative to the defined threshold.

#### Logs
- **CloudWatch Logs**:
  - **Log Streams**: Collect and store logs from various AWS services, applications, and instances. Logs are organized into log streams within a log group.
  - **Log Groups**: Group logs for a specific application or service to manage retention and access. Configure log retention policies to control how long logs are stored.
  - **Log Insights**: Use CloudWatch Logs Insights to query and analyze log data. Write queries to extract valuable information and generate insights from log data.

- **Integration**:
  - **AWS Services**: Many AWS services (e.g., Lambda, EC2, RDS) can send logs to CloudWatch Logs for centralized monitoring and troubleshooting.
  - **Custom Logs**: Applications can use the CloudWatch Logs agent or SDKs to send logs to CloudWatch for storage and analysis.

#### Dashboards
- **Creation**:
  - **Custom Dashboards**: Create CloudWatch Dashboards to visualize and monitor metrics and logs. Dashboards provide a graphical representation of key metrics and can include graphs, text widgets, and other visual elements.
  - **Widgets**: Add various types of widgets to dashboards, such as line charts, stacked area charts, and number displays. Widgets can display metrics, alarms, and log data.
  - **Customizable Views**: Customize dashboard layouts and views to focus on specific metrics, logs, or systems. Create multiple dashboards to represent different aspects of your environment.

- **Sharing**:
  - **Access Control**: Share dashboards with other AWS users or teams within your organization. Use IAM policies to control access to dashboards and their underlying data.
  - **Cross-Account**: Share dashboards across AWS accounts using resource sharing mechanisms or by setting up cross-account access.

- **Monitoring**:
  - **Real-Time Monitoring**: Use dashboards for real-time monitoring of your AWS resources. Set up widgets to display live data and update in real time.
  - **Historical Data**: Analyze historical data and trends through dashboards to understand performance patterns and identify potential issues.

---

 
 

### CloudTrail

#### Event Logging
- **Overview**:
  - **AWS CloudTrail**: A service that enables governance, compliance, and operational and risk auditing of your AWS account. CloudTrail records AWS API calls made on your account and delivers log files to an Amazon S3 bucket.

- **Configuration**:
  - **Trail Creation**: Create a trail to start logging events. You can create a trail for all regions or a specific region. This ensures that all API calls made to AWS services are recorded.
  - **Log Storage**: Configure a dedicated S3 bucket for CloudTrail logs. Ensure that bucket policies and IAM roles are set up to allow CloudTrail to write logs to the bucket.
  - **Log File Integrity**: Enable log file validation to ensure the integrity of your log files. CloudTrail uses a hash-based mechanism to verify that the logs have not been tampered with.

- **Event Types**:
  - **Management Events**: Capture API calls that manage AWS resources (e.g., create, delete, and modify resources).
  - **Data Events**: Capture API activity on data (e.g., object-level operations on S3 buckets or DynamoDB tables).
  - **Insight Events**: Detect unusual API activity. Insights can help identify potential security or operational issues.

- **Log Retrieval**:
  - **S3 Bucket**: Access and retrieve CloudTrail logs from the S3 bucket where they are stored. Logs are organized by year, month, and day.
  - **CloudWatch Logs**: Optionally, you can configure CloudTrail to deliver logs to CloudWatch Logs for real-time analysis and monitoring.

#### Insights
- **CloudTrail Insights**:
  - **Purpose**: Provides an additional layer of visibility by detecting unusual API activity. Insights use machine learning to identify and alert on anomalies in your API usage patterns.
  - **Enabling Insights**: Enable CloudTrail Insights on a trail to start analyzing API activity. Insights are available for management events and provide a summary of unusual activities.
  
- **Types of Insights**:
  - **Anomaly Detection**: Automatically detects deviations from normal API activity patterns. Examples include sudden spikes in API calls or unusual patterns in data access.
  - **Alerts**: Generate alerts when anomalies are detected. Alerts can be viewed in the CloudTrail console or forwarded to CloudWatch Events for further processing.

- **Integration and Analysis**:
  - **CloudWatch Events**: Integrate CloudTrail Insights with CloudWatch Events to create automated responses or notifications when specific anomalies are detected.
  - **Detailed Analysis**: Use the CloudTrail console to view detailed reports and analysis of detected anomalies. Analyze patterns and determine if the anomalies are indicative of potential security threats.

- **Best Practices**:
  - **Regular Review**: Regularly review CloudTrail logs and Insights reports to ensure that there are no suspicious activities or unauthorized access.
  - **Compliance and Auditing**: Utilize CloudTrail for compliance auditing and to meet regulatory requirements. Ensure that trails are configured to capture all necessary data for auditing purposes.

---

 

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
