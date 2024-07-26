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


#### EC2 (Elastic Compute Cloud)
- **Overview**:
  - **EC2**: Provides scalable virtual servers in the cloud. You can launch instances based on a variety of configurations, including different operating systems and instance types.

- **Instance Types**:
  - **General Purpose**: Balanced compute, memory, and networking resources (e.g., t4g, m5).
  - **Compute Optimized**: High-performance processors for compute-intensive tasks (e.g., c5).
  - **Memory Optimized**: Optimized for memory-intensive applications (e.g., r5, x1).
  - **Storage Optimized**: High storage throughput and capacity (e.g., i3, d2).
  - **Accelerated Computing**: Instances with GPU capabilities for tasks like machine learning (e.g., p3, g4).

- **Features**:
  - **Auto Scaling**: Automatically adjust the number of EC2 instances based on demand.
  - **Elastic Load Balancing (ELB)**: Distributes incoming traffic across multiple instances.
  - **Security Groups**: Virtual firewalls to control inbound and outbound traffic.
  - **Key Pairs**: Securely access EC2 instances via SSH using key pairs.

- **Storage**:
  - **EBS (Elastic Block Store)**: Persistent block storage that can be attached to EC2 instances.
  - **Instance Store**: Temporary storage that is physically attached to the host machine.

- **Networking**:
  - **VPC (Virtual Private Cloud)**: Isolate EC2 instances within a private network.
  - **Elastic IPs**: Static IP addresses that can be associated with EC2 instances.

#### Lambda
- **Overview**:
  - **AWS Lambda**: A serverless compute service that runs code in response to events and automatically manages the underlying compute resources.

- **Features**:
  - **Event-Driven**: Executes code in response to triggers from AWS services like S3, DynamoDB, and SNS.
  - **Automatic Scaling**: Scales automatically based on the number of incoming requests or events.
  - **Pay-As-You-Go**: You pay only for the compute time consumed by your code.

- **Deployment**:
  - **Function Code**: Write code in languages such as Python, Node.js, Java, and C#.
  - **Layers**: Package and share common code and libraries across multiple functions.

- **Integrations**:
  - **API Gateway**: Create RESTful APIs that trigger Lambda functions.
  - **Event Sources**: Integrate with services like S3, DynamoDB Streams, and Kinesis.

#### Elastic Beanstalk
- **Overview**:
  - **Elastic Beanstalk**: A platform-as-a-service (PaaS) that simplifies the deployment and management of applications. It handles the infrastructure, scaling, and monitoring of your applications.

- **Features**:
  - **Support for Multiple Languages**: Deploy applications written in Java, .NET, PHP, Node.js, Python, Ruby, and Go.
  - **Environment Management**: Manage environments with different configurations (e.g., development, staging, production).
  - **Automatic Scaling**: Automatically scales application instances based on traffic.

- **Deployment**:
  - **Deployment Options**: Use the AWS Management Console, CLI, or API to deploy applications.
  - **Configuration**: Configure application settings and environment variables via the console or configuration files.

- **Monitoring**:
  - **Health Monitoring**: Elastic Beanstalk provides built-in monitoring for application health and performance.

#### ECS (Elastic Container Service)
- **Overview**:
  - **Amazon ECS**: A fully managed container orchestration service that supports Docker containers. It allows you to easily deploy and manage containers on a cluster of EC2 instances or Fargate.

- **Features**:
  - **Task Definitions**: Define and configure Docker container settings and resource requirements.
  - **Services**: Manage long-running applications and ensure that a specified number of tasks are running at all times.
  - **Clusters**: Group of EC2 instances or Fargate tasks that run your containerized applications.

- **Integration**:
  - **Fargate**: Serverless compute engine for ECS that allows you to run containers without managing the underlying infrastructure.
  - **Load Balancing**: Use ELB to distribute traffic across ECS tasks.

- **Security**:
  - **IAM Roles**: Control access to AWS resources from within containers.

#### EKS (Elastic Kubernetes Service)
- **Overview**:
  - **Amazon EKS**: A fully managed Kubernetes service that makes it easy to run Kubernetes on AWS without needing to install and operate your own Kubernetes control plane.

- **Features**:
  - **Managed Control Plane**: AWS manages the Kubernetes control plane, including the API server and etcd.
  - **Worker Nodes**: Deploy and manage Kubernetes worker nodes (EC2 instances or Fargate).
  - **Integration**: Integrate with AWS services such as IAM, VPC, and CloudWatch for monitoring and security.

- **Kubernetes Features**:
  - **Namespaces**: Organize resources and applications within your Kubernetes cluster.
  - **Pods**: Run one or more containers within a Kubernetes pod.
  - **Services**: Define how to access and load balance traffic to your pods.

- **Scaling**:
  - **Auto Scaling**: Automatically adjust the number of worker nodes based on demand.

---

 


### Storage

#### [S3 (Simple Storage Service)](##storage-s3)

**Overview:**
Amazon S3 is an object storage service that offers scalability, data availability, security, and performance.

**Key Features:**
- **Storage Classes**: Standard, Intelligent-Tiering, Standard-IA, One Zone-IA, Glacier, and Glacier Deep Archive.
- **Data Management**: Lifecycle policies, versioning, object tagging, and cross-region replication.
- **Access Control**: Bucket policies, IAM policies, ACLs, and pre-signed URLs.
- **Data Transfer**: Multipart upload, S3 Transfer Acceleration, and AWS Snowball.
- **Security**: Server-side encryption (SSE-S3, SSE-KMS, SSE-C), client-side encryption, and bucket policies.
- **Event Notifications**: S3 Event Notifications to trigger AWS Lambda, SQS, and SNS.

**Use Cases:**
- Backup and restore
- Data lakes and big data analytics
- Static website hosting
- Content storage and distribution

**Best Practices:**
- Use S3 Transfer Acceleration for faster uploads.
- Implement lifecycle policies to transition objects to cheaper storage classes.
- Enable versioning to protect against accidental deletions.
- Use IAM roles and policies for fine-grained access control.

---

#### [EBS (Elastic Block Store)](##storage-ebs)

**Overview:**
Amazon EBS provides block-level storage volumes for use with EC2 instances.

**Key Features:**
- **Volume Types**: General Purpose SSD (gp2/gp3), Provisioned IOPS SSD (io1/io2), Throughput Optimized HDD (st1), and Cold HDD (sc1).
- **Snapshots**: Incremental backups of EBS volumes to Amazon S3.
- **Encryption**: Data at rest encryption using AWS KMS.
- **Performance**: High IOPS and low-latency access to data.
- **Resilience**: Replicated within the same Availability Zone.

**Use Cases:**
- Databases
- Enterprise applications
- Big data analytics
- File systems and media workflows

**Best Practices:**
- Select the appropriate volume type based on performance requirements.
- Regularly create snapshots for backup and disaster recovery.
- Use EBS-optimized instances for improved performance.
- Encrypt sensitive data using EBS encryption.

---

#### [EFS (Elastic File System)](##storage-efs)

**Overview:**
Amazon EFS is a scalable, fully managed file storage service for use with AWS Cloud services and on-premises resources.

**Key Features:**
- **Scalability**: Automatically scales up and down as files are added or removed.
- **Performance Modes**: General Purpose and Max I/O.
- **Storage Classes**: Standard and Infrequent Access.
- **Mount Targets**: Accessible from multiple EC2 instances within the same VPC.
- **Encryption**: Data at rest and in transit encryption using AWS KMS.
- **Access Control**: POSIX permissions, NFSv4 ACLs, and IAM policies.

**Use Cases:**
- Content management and web serving
- Home directories
- Big data and analytics
- Media processing workflows

**Best Practices:**
- Choose the appropriate performance mode based on workload requirements.
- Use lifecycle management to transition files to Infrequent Access storage class.
- Implement security best practices, including encryption and access controls.
- Monitor and optimize performance using Amazon CloudWatch metrics.

---

#### [Glacier](##storage-glacier)

**Overview:**
Amazon Glacier and Glacier Deep Archive are low-cost cloud storage services for data archiving and long-term backup.

**Key Features:**
- **Storage Classes**: Glacier and Glacier Deep Archive.
- **Retrieval Options**: Expedited, Standard, and Bulk retrievals.
- **Vault Lock**: Enforce compliance controls with a vault lock policy.
- **Security**: Data at rest encryption using AWS KMS.
- **Cost**: Extremely low-cost storage for infrequently accessed data.

**Use Cases:**
- Long-term data archiving
- Regulatory and compliance data retention
- Media asset archiving
- Backup and disaster recovery

**Best Practices:**
- Use Glacier for data that requires occasional access with flexible retrieval times.
- Use Glacier Deep Archive for data that is rarely accessed and can tolerate longer retrieval times.
- Implement lifecycle policies to automatically transition data from S3 to Glacier.
- Use Vault Lock for immutable archives to comply with regulatory requirements.

### Database

#### [RDS (Relational Database Service)](##database-rds)

**Overview:**
Amazon RDS is a managed relational database service that supports several database engines, including MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server.

**Key Features:**
- **Automated Backups**: Automatic daily backups and the ability to create manual snapshots.
- **High Availability**: Multi-AZ deployments for failover support.
- **Scalability**: Vertical scaling by changing instance types, and read replicas for horizontal scaling.
- **Security**: Encryption at rest and in transit, network isolation using VPC, and IAM integration for access control.
- **Monitoring and Metrics**: Integration with CloudWatch for performance and operational monitoring.
- **Maintenance**: Automatic patching of the database engine.

**Use Cases:**
- Web and mobile applications
- E-commerce platforms
- Enterprise applications
- Data warehousing

**Best Practices:**
- Use Multi-AZ deployments for production databases to ensure high availability.
- Implement read replicas for read-heavy workloads to improve performance.
- Regularly back up databases and test the restoration process.
- Encrypt sensitive data and use IAM roles for access control.

---

#### [DynamoDB](##database-dynamodb)

**Overview:**
Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.

**Key Features:**
- **Flexible Schema**: NoSQL data model that supports key-value and document data structures.
- **Performance**: Single-digit millisecond response times with SSD-backed storage.
- **Scalability**: Automatically scales throughput capacity to meet application demands.
- **Global Tables**: Multi-region, fully replicated tables for global applications.
- **Streams**: DynamoDB Streams to capture item-level changes for real-time processing.
- **Transactions**: ACID transactions for coordinated, all-or-nothing operations.
- **Security**: Encryption at rest, IAM policies, and VPC endpoint support.

**Use Cases:**
- Mobile and web backends
- Gaming applications
- IoT applications
- Real-time bidding platforms

**Best Practices:**
- Design tables with the appropriate partition key and sort key to optimize performance.
- Use Global Secondary Indexes (GSIs) and Local Secondary Indexes (LSIs) for query flexibility.
- Monitor and adjust read and write capacity units to manage costs and performance.
- Enable DynamoDB Streams for change data capture and real-time analytics.

---

#### [Redshift](##database-redshift)

**Overview:**
Amazon Redshift is a fully managed data warehouse service that makes it simple and cost-effective to analyze all your data using standard SQL and existing business intelligence tools.

**Key Features:**
- **Scalability**: Scale up or down with a few clicks, and pay only for what you use.
- **Performance**: Columnar storage, data compression, and parallel query execution.
- **Security**: Encryption at rest and in transit, VPC isolation, and IAM integration.
- **Data Integration**: Seamless integration with AWS data lake services and tools like Amazon S3, DynamoDB, and EMR.
- **Concurrency Scaling**: Automatically adds and removes capacity to handle unpredictable demand.
- **Data Sharing**: Securely share live data across Amazon Redshift clusters without the need to copy or move data.

**Use Cases:**
- Business intelligence
- Big data analytics
- ETL processes
- Data lake integration

**Best Practices:**
- Use columnar storage for fast query performance and data compression.
- Regularly vacuum and analyze tables to maintain performance.
- Use workload management (WLM) to prioritize and manage query workloads.
- Secure data by enabling encryption and configuring appropriate IAM policies.

---

#### [Aurora](##database-aurora)

**Overview:**
Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud, combining the performance and availability of high-end commercial databases with the simplicity and cost-effectiveness of open-source databases.

**Key Features:**
- **Performance**: Up to 5 times faster than standard MySQL databases and 3 times faster than standard PostgreSQL databases.
- **Scalability**: Automatically scales storage up to 128 TB per database instance.
- **High Availability**: Multi-AZ deployment with failover and read replicas.
- **Global Database**: Disaster recovery and low-latency reads with multi-region read replicas.
- **Security**: Encryption at rest and in transit, IAM integration, and network isolation with VPC.
- **Backup and Restore**: Continuous backups to Amazon S3 and point-in-time recovery.

**Use Cases:**
- Enterprise applications
- SaaS applications
- Web and mobile backends
- Online gaming

**Best Practices:**
- Use Aurora Serverless for variable workloads to automatically scale compute capacity.
- Implement read replicas to offload read traffic and improve performance.
- Regularly back up your databases and test restoration procedures.
- Enable encryption and use IAM roles for access control and security.

### Networking

#### [VPC (Virtual Private Cloud)](##networking-vpc)

**Overview:**
Amazon VPC allows you to provision a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define.

**Key Features:**
- **Subnets**: Public and private subnets to organize resources.
- **Routing**: Route tables to manage traffic routing within the VPC.
- **Internet Gateway**: Allows access to the internet from the VPC.
- **NAT Gateway**: Enables instances in a private subnet to connect to the internet while preventing inbound traffic from the internet.
- **VPC Peering**: Connects VPCs, allowing traffic to route between them using private IP addresses.
- **VPC Endpoints**: Private connections to AWS services without requiring an internet gateway or NAT device.
- **Security**: Security groups and network ACLs to control inbound and outbound traffic at the instance and subnet levels.
- **Flow Logs**: Captures information about the IP traffic going to and from network interfaces in your VPC.

**Use Cases:**
- Host web applications
- Isolate environments for security
- Extend on-premises networks to the cloud
- Data analytics and big data workloads

**Best Practices:**
- Design VPCs with multiple subnets across different Availability Zones for high availability.
- Use security groups and network ACLs to implement a layered security approach.
- Implement VPC endpoints to privately connect to AWS services.
- Monitor network traffic using VPC Flow Logs and AWS CloudWatch.

---

#### [Route 53](##networking-route-53)

**Overview:**
Amazon Route 53 is a scalable Domain Name System (DNS) web service designed to route end users to internet applications by translating human-readable names like www.example.com into IP addresses.

**Key Features:**
- **DNS Management**: Register domain names and manage DNS records.
- **Traffic Routing**: Policies include simple, weighted, latency-based, failover, geolocation, and geoproximity routing.
- **Health Checks**: Monitor the health and performance of resources and route traffic based on health check status.
- **Domain Registration**: Register and manage domain names directly through Route 53.
- **DNSSEC**: Domain Name System Security Extensions to protect against DNS spoofing.

**Use Cases:**
- Manage DNS for web applications
- Implement global load balancing
- Route traffic based on health checks
- Register and manage domain names

**Best Practices:**
- Use health checks and failover routing to improve the availability of applications.
- Implement DNSSEC to enhance security.
- Use latency-based routing to route traffic to the nearest endpoint for better performance.
- Regularly review and update DNS records to reflect current infrastructure.

---

#### [CloudFront](##networking-cloudfront)

**Overview:**
Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds.

**Key Features:**
- **Edge Locations**: Global network of edge locations to cache content close to users.
- **Caching**: Configurable cache behaviors and TTL settings.
- **Security**: HTTPS support, AWS WAF integration, and DDoS protection.
- **Origin Sources**: Supports multiple origins including S3, EC2, and custom origins.
- **Content Delivery**: Real-time video streaming, dynamic content, and static content.
- **Access Control**: Geo-restriction, signed URLs, and signed cookies for content access control.

**Use Cases:**
- Accelerate the delivery of static and dynamic web content
- Stream live and on-demand video
- Distribute software downloads
- Serve web applications securely

**Best Practices:**
- Optimize cache behavior and TTL settings for frequently accessed content.
- Use signed URLs and cookies to control access to content.
- Implement AWS WAF to protect against web exploits.
- Monitor CloudFront performance and usage with CloudWatch.

---

#### [Direct Connect](##networking-direct-connect)

**Overview:**
AWS Direct Connect is a network service that provides an alternative to using the internet to connect customers' on-premises environments to AWS.

**Key Features:**
- **Dedicated Connections**: Provides a dedicated network connection from your premises to AWS.
- **High Bandwidth**: Supports high bandwidth connections, reducing latency and increasing reliability.
- **Private Connectivity**: Establishes a private connection to your VPCs, bypassing the public internet.
- **Link Aggregation**: Supports LAG (Link Aggregation Groups) to combine multiple connections for increased bandwidth.
- **Virtual Interfaces**: Public and private virtual interfaces to access public AWS services or VPCs.

**Use Cases:**
- Hybrid cloud deployments
- Data center migrations
- High-volume data transfers
- Consistent and low-latency network performance

**Best Practices:**
- Plan and implement redundancy for high availability.
- Use Direct Connect Gateway to connect multiple VPCs across regions.
- Monitor network performance and utilization.
- Secure the connection using AWS VPN or other encryption methods for data in transit.

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
