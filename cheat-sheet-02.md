 
---
![Untitled-1 md 1](https://github.com/user-attachments/assets/b41125ae-f487-48ac-9b7e-dbc2295035c6)

## Disaster Recovery (DR) Approaches

- **Backup and Restore**  
  Lowest cost. Just create backups.

- **Pilot Light**  
  Small part of core services is running and syncing data or documents.

- **Warm Standby**  
  Scaled-down version of a fully functional environment that is actively running.

- **Multi-Site**  
  On-premises and in AWS in an active-active configuration.

- **Cross-Region Disaster Recovery**  
  Create an AMI from your EC2 instance and copy it to a second region.

---

## Storage
![Untitled-1 md 4](https://github.com/user-attachments/assets/6ed71ff5-da90-4455-8283-3e154564ed71)

### Instance Store

- **Description**  
  Block-level storage physically attached to the host computer. Temporary/ephemeral storage.

- **Use Cases**  
  - Temp info that changes frequently (e.g., caches, buffers).
  - Data replicated across instances where losing a copy occasionally is acceptable.

- **Characteristics**  
  - High performance and low latency.
  - Cost included in instance cost.
  - Data is lost if the instance is stopped or terminated.

### EBS (Elastic Block Store)
![Untitled-1 md 5](https://github.com/user-attachments/assets/2f09ea1c-ff13-47bf-9c0b-2ac2aa4d8a6c)

- **Types of Volumes**  
  - **General Purpose SSD (gp2, gp3)**: Low-latency interactive apps, dev/test environments.
  - **Provisioned IOPS SSD (io1, io2)**: Sub-millisecond latency, sustained IOPS performance.
  - **EBS Cold HDD (sc1)**: Lowest cost for infrequently accessed data.
  - **EBS Throughput Optimized HDD (st1)**: Frequent access and throughput-intensive workloads.

- **Features**  
  - EBS cannot attach to multiple AZs (new multi-attach feature is single AZ, certain SSD volumes).
  - Use EBS Data Lifecycle Manager (DLM) for managing backup snapshots.
  - EBS supports encryption of data at rest and in transit.

- **Note**  
  - iSCSI (block protocol) vs. NFS (file protocol).
  - Consider replacing multiple EBS volumes with EFS for shared storage.

### EFS (Elastic File System)

- **Features**  
  - Attach to many instances across multiple AZs.
  - Fully managed, auto-scales.
  - Linux only (POSIX permissions).

- **Storage Classes**  
  - Transition unused data to EFS IA (Infrequent Access).

- **Security**  
  - Protected by EFS Security Groups.

### S3 (Simple Storage Service)

- **Characteristics**  
  - Durability of 99.999999999%.
  - Enable versioning and MFA Delete for buckets.

- **Lifecycle Actions**  
  - **Transition Actions**: Define when to move to another storage class.
  - **Expiration Actions**: Delete objects after a period.

- **Storage Classes**  
  - **Standard-IA**: Multi-AZ.
  - **One Zone-IA**: Single AZ.

- **Special Features**  
  - Pre-signed URLs for secure access.
  - Data must pass through S3 before moving to Glacier.
  - Multi-part upload for large files.

### Glacier

- **Features**  
  - Slow retrieval, but Expedited Retrieval can reduce time to 1-5 minutes.

### Amazon FSx

- **Types**  
  - **Windows File Server**: Multi-AZ, supports DFS, integrates with AD.
  - **FSx for Lustre**: High-performance computing (HPC), does not support Windows.

### Amazon Aurora Global Database

- **Features**  
  - Supports globally distributed applications.
  - Create Aurora replicas for read traffic.
  - Aurora Serverless automatically scales capacity.

### RDS (Relational Database Service)
![Untitled-1 md 6](https://github.com/user-attachments/assets/aaeb6d4a-adcc-495e-a61f-6b9c1d08dcf6)

- **Features**  
  - **Transactional DB (OLTP)**.
  - Create RDS read replicas for read-heavy workloads.
  - Multi-AZ for synchronous replication.
  - Encrypt existing RDS databases using snapshots.
  - Point-in-time restore (PITR) for recent backups.

### ElastiCache
![Untitled-1 md 7](https://github.com/user-attachments/assets/98e54a1a-bc80-4567-847f-1cfd36010838)

- **Types**  
  - **Redis**: Replication, high availability, token protection, optional in-transit encryption.
  - **Memcached**: Multi-core multi-threaded.

- **Use Cases**  
  - Improve performance by caching database queries or S3 data.

### DynamoDB
 
![Untitled-1 md 8](https://github.com/user-attachments/assets/d439f378-f344-48ae-98d2-b3f875284dd9)

- **Features**  
  - Key/value storage with millisecond performance.
  - No read replicas; use DAX for caching.
  - Measures RCUs (read capacity units) and WCUs (write capacity units).
  - Auto-scaling with AWS Application Auto Scaling.

- **Best Practices**  
  - Keep item sizes small (<400 KB).
  - Store frequently accessed data in separate tables.
  - Use timestamp-based tables for data access.

---


Here’s a Markdown-friendly overview of AWS services and concepts, with sections organized for clarity:

---

# AWS Disaster Recovery (DR) Approaches

1. **Backup and Restore**
   - Lowest cost, create backups of data and restore when needed.

2. **Pilot Light**
   - A minimal version of core services running and syncing data/documents.

3. **Warm Standby**
   - A scaled-down version of a fully functional environment that is actively running.

4. **Multi-Site**
   - Active-active configuration with both on-prem and AWS environments.

5. **Disaster Recovery Across Regions**
   - Create an AMI from your EC2 instance and copy it to a second region.

---

# AWS Storage Solutions

## Instance Store
- **Characteristics:**
  - Block-level storage physically attached to the host.
  - Temporary/ephemeral, high performance, low latency.
  - Ideal for temporary data and caches.
  - Data is lost if the instance stops or terminates.

## EBS (Elastic Block Store)
- **Types:**
  - **General Purpose SSD (gp2, gp3):** For low-latency apps, dev/test.
  - **Provisioned IOPS SSD (io1, io2):** For sub-millisecond latency and high performance.
  - **Cold HDD (sc1):** Lowest cost for infrequent access.
  - **Throughput Optimized HDD (st1):** For throughput-intensive workloads.
- **Notes:**
  - Not inherently multi-AZ; consider EFS for shared storage.
  - Supports encryption at rest and in transit.

## EFS (Elastic File System)
- **Characteristics:**
  - Fully managed, auto-scaling.
  - Attach to multiple instances across multiple AZs.
  - Linux only, supports POSIX permissions.
  - Data can be transitioned to EFS IA for cost savings.

## S3 (Simple Storage Service)
- **Features:**
  - **Durability:** 99.999999999%.
  - **Versioning & MFA Delete:** Best practices.
  - **Lifecycle Policies:**
    - **Transition Actions:** Move to other storage classes.
    - **Expiration Actions:** Auto-delete objects.
  - **Intelligent Tiering:** Cost-effective storage.
  - **Pre-Signed URLs:** Secure access to objects.
  - **Glacier:** Low-cost archival storage with retrieval options.

## Glacier
- **Retrieval Options:**
  - **Standard:** Retrieval in minutes to hours.
  - **Expedited Retrieval:** 1-5 minutes.

## Amazon FSx
- **Types:**
  - **FSx for Windows File Server:** Multi-AZ, DFS, integrates with AD.
  - **FSx for Lustre:** High-performance computing, not Windows-compatible.

---

# Data Migration and Copying

## AWS Schema Conversion Tool (SCT)
- Convert DB schemas between different types (e.g., Oracle to Redshift).

## Database Migration Service (DMS)
- Copy databases. Can be used after SCT for schema conversion.

## AWS DataSync
- Copy large amounts of data from on-prem to AWS storage solutions (e.g., S3, EFS).

---

# Analytics (OLAP)

## Amazon Redshift
- **Purpose:** Columnar data warehouse for complex queries on structured data.
- **Redshift Spectrum:** Query S3 data with Redshift.

## Amazon Athena
- **Purpose:** Serverless SQL queries on S3 data.
- **Integration:** Works with client-side and server-side encryption.

## Amazon S3 Select
- Analyze and process data directly from S3 using SQL.

---

# Services for Architecture

## Amazon SQS (Simple Queue Service)
- **Types:**
  - **Standard Queues:** Unlimited throughput, best-effort ordering.
  - **FIFO Queues:** Ordered messages, limited throughput.
- **Features:**
  - **Polling:** Short vs. long polling.
  - **Batching:** For efficiency.
  - **Visibility Timeout:** Ensures message processing.

## Amazon SNS (Simple Notification Service)
- Fully managed service for pushing notifications to multiple services.

## Amazon Kinesis
- **Purpose:** Real-time data ingestion (e.g., IoT sensor data).
- **Components:**
  - **Shards:** Store data records.
  - **Partition Keys:** Group data by shard.

## Amazon API Gateway
- **Features:**
  - **Throttling Limits:** Configure server-side, per-method, per-client, and account-level limits.
  - **API Caching:** Configurable TTL (default 300 seconds).

## Amazon CloudFront
- **Purpose:** Content delivery network (CDN) to distribute files.
- **Features:**
  - **Origin Access Identity (OAI):** Secure S3 content access.
  - **Lambda@Edge:** Run code closer to users.
  - **Field-Level Encryption:** Secure sensitive data.

## AWS Global Accelerator
- **Purpose:** Improve availability and performance across regions.
- **Features:**
  - Provides 2 static IPs anycast from AWS edge network.

## AWS STS (Security Token Service)
- **Uses:**
  - **Federation:** Temporary access using SAML 2.0.
  - **Single Sign-On (SSO):** Custom identity broker for SSO.

## Amazon ECS (Elastic Container Service)
- **Types:**
  - **Fargate:** Serverless, managed.
  - **EC2:** Direct instance access.

---

# Security

## Encryption
- **Data at Rest:**
  - **Client-Side Encryption:** Use KMS or application-managed keys.
  - **Server-Side Encryption:** 
    - **SSE-C:** Customer-provided keys.
    - **SSE-S3:** Amazon-managed keys.
    - **SSE-KMS:** KMS-managed keys.
    - **CloudHSM:** Your own encryption keys.
- **Data in Motion:**
  - **SSL/TLS:** Encrypts data in transit.

## Amazon GuardDuty
- Use with CloudWatch and SNS for security alerts.

## IAM (Identity and Access Management)
- **Permissions Boundary:** Limits maximum permissions for users/roles.

## AWS CloudTrail
- **Purpose:** Audit trail of API calls.
- **Logs:**
  - **Data Events:** Resource operations.
  - **Management Events:** Resource management.

## AWS Accounts
- Use **Service Control Policies (SCPs)** for multiple accounts, **IAM policies** for single accounts.

---

# Additional AWS Services

- **AWS App Mesh:** Application networking for microservices.
- **AWS Resource Access Manager:** Share Transit Gateway connections.
- **AWS Server Migration Service (SMS):** Migrate VMs.
- **AWS Step Functions:** Coordinate serverless workflows.
- **AWS Elastic Beanstalk:** PaaS for app deployment.
- **AWS Simple Workflow Service (SWF):** Task execution.
- **AWS CodeStar:** Develop, build, deploy applications.
- **AWS Config:** Manage resource configurations.
- **AWS Batch:** Batch processing of jobs.
- **Amazon Lex:** Conversational interfaces.
- **AWS X-Ray:** Analyze and debug serverless apps.
- **Amazon EMR:** Data processing with Hadoop.
- **AWS Import/Export:** Data transfer via HDDs.
- **Amazon Connect:** Call center service.
- **Amazon SES:** Email service for marketing.
- **Amazon QuickSight:** Business intelligence.
- **Amazon Elasticsearch Service:** Operational analytics.
- **Amazon Neptune:** Graph databases.
- **AWS AppStream:** Application streaming.
- **Amazon Kinesis:** Streaming data collection.
- **Amazon Elastic Transcoder:** Media file conversion.
- **CloudSearch:** Search engine service.
- **AWS CLI:** Command-line interface for AWS.
- **AWS LightSail:** Simplified virtual servers and databases.
- **Amazon MSK:** Managed Kafka.
- **AWS IoT Core:** IoT device management.
- **Amazon Cognito:** Authentication for mobile and web apps.

---

 
