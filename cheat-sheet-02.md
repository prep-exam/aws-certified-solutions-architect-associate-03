Here’s a Markdown-formatted version of the content, organized for clarity and readability:

---

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

- **Features**  
  - **Transactional DB (OLTP)**.
  - Create RDS read replicas for read-heavy workloads.
  - Multi-AZ for synchronous replication.
  - Encrypt existing RDS databases using snapshots.
  - Point-in-time restore (PITR) for recent backups.

### ElastiCache

- **Types**  
  - **Redis**: Replication, high availability, token protection, optional in-transit encryption.
  - **Memcached**: Multi-core multi-threaded.

- **Use Cases**  
  - Improve performance by caching database queries or S3 data.

### DynamoDB

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

 