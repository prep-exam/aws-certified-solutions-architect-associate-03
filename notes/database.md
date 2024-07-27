Certainly! Here’s your cheat sheet with Markdown formatting and color for headings:

---

### <span style="color:blue">Database</span>

**<span style="color:darkorange">RDS (Relational Database Service)</span>**
- **Description:** 
  - AWS Managed Service to create PostgreSQL, MySQL, MariaDB, Oracle, Microsoft SQL Server, and Amazon Aurora in the cloud.
- **Scalability:** 
  - Up to **5 Read Replicas**: Replication is asynchronous (eventually consistent reads).
- **Availability:**
  - **Multi-AZ Deployment**: For synchronous replication.
  - **Cross-Region Read Replicas**: Replication costs apply; no cost for cross-AZ.
  - **Automatic Failover**: Switches CNAME from primary to standby database.
- **Authentication:**
  - **Password and IAM Database Authentication** (MySQL, PostgreSQL).
- **Monitoring:**
  - **Enhanced Monitoring**: Tracks CPU and memory usage by each DB process.
- **Backup:**
  - **Automated Backup**: 1 to 35 days retention (AWS Backup for 90 days).
- **Encryption:**
  - **Encrypting Unencrypted DB Instances**: Snapshot → Copy → Encrypt → Restore.

**<span style="color:green">Amazon Aurora</span>**
- **Description:** 
  - Fully managed relational database compatible with MySQL and PostgreSQL.
- **Performance:**
  - **5x Throughput of MySQL**.
  - **3x Throughput of PostgreSQL**.
- **Aurora Global Database:**
  - **Spans Multiple AWS Regions**: Low-latency global reads.
  - **Disaster Recovery**: RPO of 1 second and RTO of 1 minute.
- **Aurora Serverless:**
  - **On-Demand Auto-Scaling**: For intermittent, unpredictable workloads.
- **Architecture:**
  - **DB Cluster**: With cluster volume in multiple AZs.
  - **Primary DB Instance**: Supports both read and write.
  - **Aurora Replica**: Up to 15 replicas, supports only read, automatic failover.
- **Connection Endpoints:**
  - **Cluster Endpoint**: Connects to primary DB instance, for write operations.
  - **Reader Endpoint**: Load-balances read-only connections to replicas.
  - **Custom Endpoint**: Up to 5 endpoints for specialized workloads.
  - **Instance Endpoint**: Connects to a specific DB instance, used for improving speed post-failover.

---
### <span style="color:blue">DynamoDB</span>
- **Description:**
  - AWS proprietary, serverless, managed NoSQL database.
  - Stores JSON documents or session data.
  - Distributed serverless cache with single-digit millisecond performance.
- **Capacity Modes:**
  - **Planned Capacity:**
    - **WCU & RCU**: Provisioned capacity, auto-scaling enabled.
    - **Good for predictable workloads**.
  - **On-Demand Capacity:**
    - **Unlimited WCU & RCU**: Higher cost, suitable for unpredictable workloads with low throughput.
- **DynamoDB Accelerator (DAX):**
  - Caches frequently read values.
  - Offloads heavy read operations and prevents `ProvisionedThroughputExceededException`.
- **Streams:**
  - Enable DynamoDB Streams to trigger events and integrate with Lambda functions (e.g., send a welcome email).
- **Global Tables:**
  - Serves data globally; requires DynamoDB Streams.
- **Migration:**
  - Use Amazon DMS (Data Migration Service) to migrate from MongoDB, Oracle, MySQL, S3, etc., to DynamoDB.

##### <span style="color:green">**ElastiCache**</span>
- **Description:**
  - AWS Managed Service for Redis or Memcached.
  - Used as distributed cache with sub-millisecond performance.
- **ElastiCache for Redis:**
  - **Features:**
    - Multi-AZ with auto-failover.
    - Cluster mode support.
    - Access using Redis Auth (password/token).
    - **HIPAA Compliant**.
- **ElastiCache for Memcached:**
  - **Intended Use:**
    - Speeds up dynamic web applications.
    - **Not HIPAA Compliant**.

##### <span style="color:orange">**Redshift**</span>
- **Description:**
  - Columnar database, OLAP (Online Analytical Processing).
  - Supports massive parallel query execution (MPP).
  - Used for data analytics and data warehousing.
- **Integration:**
  - **Business Intelligence (BI) Tools**: Integrates with AWS QuickSight, Tableau.
- **Redshift Spectrum:**
  - Queries data in S3 buckets directly without loading data into Redshift.
 
##### <span style="color:purple">Amazon Kinesis</span>
- **Description:**
  - Fully managed service for collecting, processing, and analyzing streaming real-time data.
  - Common use cases: IoT devices, gaming applications, vehicle tracking, clickstream.
- **Components:**
  - **Kinesis Data Streams:**
    - **Producer:** Amazon Kinesis Agent, SDK, Kinesis Producer Library (KPL).
    - **Consumer:** Kinesis Data Analytics, Kinesis Data Firehose, Kinesis Consumer Library (KCL).
    - **Data Retention:** 24 hours (default) to 365 days (max).
    - **Order:** Maintained at Shard (partition) level.
  - **Kinesis Data Firehose:**
    - **Function:** Loads data streams into AWS data stores such as S3, Amazon Redshift, and Elasticsearch.
    - **Transformation:** Use Lambda functions to transform data.
    - **Error Handling:** Store failed data in another S3 bucket.
  - **Kinesis Data Analytics:**
    - **Function:** Analyzes data streams with SQL or Apache Flink.
  - **Kinesis Video Streams:**
    - **Function:** Capture, process, and store video streams.

##### <span style="color:blue">Amazon EMR</span>
- **Description:**
  - Elastic MapReduce (EMR): Big data cloud platform for processing vast amounts of data.
  - Uses open-source tools such as Hadoop, Apache Spark, Apache Hive, Apache HBase, Apache Flink, Apache Hudi, and Presto.
- **Use Case:**
  - Data transformation workloads: Extract, Transform, Load (ETL).
  - Example: Analyze Clickstream data from S3 using Apache Spark and Hive to deliver more effective ads.

##### <span style="color:green">Neptune</span>
- **Description:**
  - Graph Database.
- **Use Case:**
  - High relationship data, social networking data, knowledge graphs (e.g., Wikipedia).

##### <span style="color:orange">Elasticsearch</span>
- **Description:**
  - Amazon-managed Elasticsearch service.
- **Integration:**
  - Integrates with Kinesis Data Firehose, AWS IoT, and CloudWatch logs.
- **Use Case:**
  - Search, indexing, partial or fuzzy search.



##### <span style="color:purple">AWS Snow Family</span>
- **Description:**
  - Used for on-premises large-scale data migration to S3 buckets and processing data at low network locations.
  - Install AWS OpsHub software to transfer files from your on-premises machine to the Snow device.
  - Direct migration to Glacier is not supported; create an S3 bucket with a lifecycle policy to move files to Glacier. Use DataSync for direct Glacier transfers.
- **Family Members:**
  - **Snowcone:**
    - **Storage:** 8TB
    - **RAM:** 4GB
    - **Migration Type:** Online & offline
    - **DataSync:** Yes
    - **Migration Size:** GBs and TBs
  - **Snowball Edge Storage Optimized:**
    - **Storage:** 80TB
    - **RAM:** 80GB
    - **Migration Type:** Offline
    - **DataSync:** No
    - **Migration Size:** Petabyte scale
  - **Snowball Edge Compute Optimized:**
    - **Storage:** 42TB
    - **RAM:** 208GB
    - **Migration Type:** Offline
    - **DataSync:** No
    - **Migration Size:** Petabyte scale
  - **Snowmobile:**
    - **Storage:** 100PB
    - **RAM:** N/A
    - **Migration Type:** Offline
    - **DataSync:** No
    - **Migration Size:** Exabyte scale

##### <span style="color:blue">AWS Storage Gateway</span>
- **Description:**
  - Hybrid cloud service to move on-premises data to the cloud and connect on-premises applications with cloud storage.
- **Types:**
  - **File Gateway:**
    - **Protocol:** NFS & SMB
    - **Backed by:** S3 -> S3-IA, S3 One Zone-IA
    - **Use Case:** Store files as objects in S3 with local cache for low-latency access, user authentication using Active Directory.
  - **FSx File Gateway:**
    - **Protocol:** SMB & NTFS
    - **Backed by:** FSx -> S3
    - **Use Case:** Windows or Lustre File Server, integration with Microsoft AD.
  - **Volume Gateway:**
    - **Protocol:** iSCSI
    - **Backed by:** S3 -> EBS
    - **Use Case:** Block storage in S3 with backups as EBS snapshots. Use Cached Volume for low-latency and Stored Volume for scheduled backups.
  - **Tape Gateway:**
    - **Protocol:** iSCSI VTL
    - **Backed by:** S3 -> S3 Glacier & Glacier Deep Archive
    - **Use Case:** Backup data in S3 and archive in Glacier using a tape-based process.

##### <span style="color:green">AWS DataSync</span>
- **Description:**
  - Used for large-scale data migration from on-premises storage systems (NFS and SMB protocols) to AWS storage (S3, EFS, FSx for Windows, Snowcone) over the internet.
  - Can be used to archive on-premises cold data directly to S3 Glacier or S3 Glacier Deep Archive.
  - Supports migration to any S3 storage class.
  - Use with Direct Connect for secure private network migration to AWS services associated with VPC endpoints.

##### <span style="color:orange">AWS Backup</span>
- **Description:**
  - Centrally manage and automate the backup process for EC2 instances, EBS Volumes, EFS, RDS databases, DynamoDB tables, FSx for Lustre, FSx for Windows Server, and Storage Gateway volumes.
- **Use Case:**
  - Automate RDS backup with a 90-day retention policy. (Direct RDS backup automation has a max 35-day retention period.)


### <span style="color:purple">Database Migration Service (DMS)</span>
- **Description:**
  - Helps migrate databases to AWS with the source remaining fully operational during migration, minimizing downtime.
  - You need to select an EC2 instance to run DMS for migrating (and replicating) databases from source to target, e.g., On-premises → AWS, AWS → AWS, or AWS → On-premises.
- **Migration Types:**
  - **Homogenous Migrations:** 
    - Example: On-premises PostgreSQL → AWS RDS PostgreSQL
  - **Heterogeneous Migrations:** 
    - Example: SQL Server or Oracle → MySQL, PostgreSQL, Aurora, Teradata or Oracle → Amazon Redshift
    - Use AWS Schema Conversion Tool (SCT) at the source for heterogeneous migrations.

### <span style="color:blue">AWS Application Migration Service (MGN)</span>
- **Description:**
  - Migrates virtual machines from VMware vSphere, Microsoft Hyper-V, or Microsoft Azure to AWS.
  - **AWS Application Migration Service (New):**
    - Utilizes continuous, block-level replication.
    - Enables cutover windows measured in minutes.
  - **AWS Server Migration Service (Legacy):**
    - Utilizes incremental, snapshot-based replication.
    - Enables cutover windows measured in hours.
