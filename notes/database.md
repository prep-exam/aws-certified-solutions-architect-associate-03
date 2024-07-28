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

Here's the updated summary with integration details added:

---

### AWS Kinesis Services Overview

---

#### **Kinesis Video Streams**
- **Purpose**: Ingests and indexes streaming video data.
- **Use Cases**: 
  - Computer vision applications
  - Streaming video
  - Two-way videoconferencing
- **Producer**: Sends video, audio, subtitles, GPS coordinates.
- **Consumer**: Pulls data for playback or processing.
- **Retention**: Default 24 hours, extendable up to 7 days.
- **Protocols Supported**: HLS, DASH, WebRTC.
- **Integration**: 
  - **Amazon Rekognition**: For video analysis and image recognition.
  - **Amazon SageMaker**: For machine learning models.
  - **AWS Lambda**: For processing video data streams.

---

#### **Kinesis Data Streams**
- **Purpose**: Aggregates, buffers, and stores data from producers until consumers process it.
- **Use Cases**: 
  - Application logs
  - Stock trades
  - Social media feeds
  - Financial transactions
  - Location tracking information
- **Producer**: Feeds data into a stream using Kinesis Agent or KPL.
- **Consumer**: Reads data records from the stream, supporting multiple consumers (fan-out).
- **Retention**: Up to 7 days.
- **Throughput**: Scales with the number of shards (1 shard = 5 read TPS, 2 MB/s; 1000 write TPS, 1 MB/s).
- **Integration**: 
  - **AWS Lambda**: For real-time data processing.
  - **Amazon EMR**: For big data processing with Hadoop.
  - **Amazon Redshift**: For data warehousing and analytics.
  - **Amazon S3**: For long-term storage and data archiving.

---

#### **Kinesis Data Firehose**
- **Purpose**: Ingests, transforms, and delivers streaming data to destinations.
- **Use Cases**: 
  - Cleaning data
  - Format conversion (e.g., JSON to Parquet)
- **Integration**: 
  - **AWS Lambda**: For data transformation.
  - **Amazon Redshift**: For data warehousing.
  - **Amazon S3**: For storage.
  - **Amazon Elasticsearch Service**: For search and analytics.
  - **Splunk**: For log and event data analysis.

---

### Comparison Table

---

| **Service**                     | **Transforms Data** | **Maximum Retention** | **Model**           | **Use Cases**                                                                                           | **Integrations**                                                                                   |
|---------------------------------|---------------------|-----------------------|---------------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **Simple Queue Service (SQS)**  | No                  | 14 days               | Producer-consumer   | Passing small, short-lived messages between application components.                                    | -                                                                                                  |
| **Kinesis Video Streams**       | No                  | 7 days                | Producer-consumer   | Ingesting and indexing streaming video data from webcams, security cameras, and smartphones.           | Amazon Rekognition, Amazon SageMaker, AWS Lambda                                                  |
| **Kinesis Data Streams**        | No                  | 7 days                | Producer-consumer   | Aggregating and storing logs, trades, social media feeds, transactions, and location data.              | AWS Lambda, Amazon EMR, Amazon Redshift, Amazon S3                                                |
| **Kinesis Data Firehose**       | Yes                 | N/A                   | Destination-specified | Transforming and delivering streaming data to Redshift, S3, Splunk, etc.                               | AWS Lambda, Amazon Redshift, Amazon S3, Amazon Elasticsearch Service, Splunk                        |

---

### Key Differences
- **SQS**: For small, short-lived messages; simple producer-consumer model.
- **Kinesis Video Streams**: For streaming video data; supports computer vision and videoconferencing; integrates with Rekognition, SageMaker, and Lambda.
- **Kinesis Data Streams**: For large data streams; supports multiple consumers and fan-out; integrates with Lambda, EMR, Redshift, and S3.
- **Kinesis Data Firehose**: For transforming and delivering data; integrates with Lambda, Redshift, S3, Elasticsearch Service, and Splunk.

---

Use these quick notes to understand the key aspects and integrations of each AWS Kinesis service!



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

---

### <span style="color:blue">AWS Snow Family</span>

**Description:**  
Used for on-premises large-scale data migration to S3 buckets and processing data at low network locations. Install AWS OpsHub software to transfer files from your on-premises machine to the Snow device. Direct migration to Glacier is not supported; create an S3 bucket with a lifecycle policy to move files to Glacier. Use DataSync for direct Glacier transfers.

#### Family Members

| **Device**                       | **Storage** | **RAM** | **Migration Type** | **DataSync** | **Migration Size** |
|----------------------------------|-------------|---------|--------------------|--------------|--------------------|
| <span style="color:green">**Snowcone**</span> | 8TB         | 4GB     | Online & Offline   | Yes          | GBs and TBs        |
| <span style="color:green">**Snowball Edge Storage Optimized**</span> | 80TB        | 80GB    | Offline            | No           | Petabyte scale     |
| <span style="color:green">**Snowball Edge Compute Optimized**</span> | 42TB        | 208GB   | Offline            | No           | Petabyte scale     |
| <span style="color:green">**Snowmobile**</span> | 100PB       | N/A     | Offline            | No           | Exabyte scale      |

---

### <span style="color:blue">AWS Storage Gateway</span>

**Description:**  
Hybrid cloud service to move on-premises data to the cloud and connect on-premises applications with cloud storage.

#### Types

| **Gateway Type**             | **Protocol** | **Backed by**                        | **Use Case**                                                                                       |
|------------------------------|--------------|--------------------------------------|-----------------------------------------------------------------------------------------------------|
| <span style="color:green">**File Gateway**</span>     | NFS & SMB     | S3 -> S3-IA, S3 One Zone-IA           | Store files as objects in S3 with local cache for low-latency access, user authentication using Active Directory. |
| <span style="color:green">**FSx File Gateway**</span>  | SMB & NTFS    | FSx -> S3                             | Windows or Lustre File Server, integration with Microsoft AD.                                        |
| <span style="color:green">**Volume Gateway**</span>   | iSCSI         | S3 -> EBS                             | Block storage in S3 with backups as EBS snapshots. Use Cached Volume for low-latency and Stored Volume for scheduled backups. |
| <span style="color:green">**Tape Gateway**</span>     | iSCSI VTL     | S3 -> S3 Glacier & Glacier Deep Archive | Backup data in S3 and archive in Glacier using a tape-based process.                                |


File Gateway presents a file-based interface to Amazon S3, which appears as a network file share. It enables you to store and retrieve Amazon S3 objects through standard file storage protocols. File Gateway allows your existing file-based applications or devices to use secure and durable cloud storage without needing to be modified. With File Gateway, your configured S3 buckets will be available as Network File System (NFS) mount points or Server Message Block (SMB) file shares.



To store the backup data from on-premises to a durable cloud storage service, you can use File Gateway to store and retrieve objects through standard file storage protocols (SMB or NFS). File Gateway enables your existing file-based applications, devices, and workflows to use Amazon S3, without modification. File Gateway securely and durably stores both file contents and metadata as objects while providing your on-premises applications low-latency access to cached data.
---
 

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
