### <span style="color:green">Amazon S3</span>

- **Description:**
  - S3 Bucket is an object-based storage used to manage data as objects.
  - **S3 Object:** 
    - **Value:** Data bytes of object (photos, videos, documents, etc.)
    - **Key:** Full path of the object in bucket e.g. `/movies/comedy/abc.avi`
    - **Version ID:** Version object, if versioning is enabled
    - **Metadata:** Additional information

- **Bucket Details:**
  - S3 Bucket holds objects. S3 console shows virtual folders based on the key.
  - S3 is a universal namespace, so bucket names must be globally unique (think like having a domain name).
    - URL: `https://<bucket-name>.s3.<aws-region>.amazonaws.com` 
    - URL: `https://s3.<aws-region>.amazonaws.com/<bucket-name>`
  - Unlimited Storage, Unlimited Objects from 0 Bytes to 5 Terabytes in size. Use multi-part upload for objects > 100MB.
  - All new buckets are private when created by default. Public access must be enabled explicitly.
  - **Access Control:**
    - Configurable using Access Control List (ACL) (deprecated) and S3 Bucket Policies (recommended).
    - S3 Bucket Policies are JSON-based for complex access rules at user, account, folder, and object levels.
  - Enable **S3 Versioning** and **MFA Delete** features to protect against accidental deletion of S3 objects.
  - **Object Lock:** Store objects using write-once-read-many (WORM) model to prevent deletion or overwriting for a fixed retention period or indefinitely (Legal Hold).

- **Website Hosting:**
  - You can host static websites on S3 bucket (HTML, CSS, client-side JavaScript, images).
  - Enable Static Website Hosting and Public Access for S3 to avoid 403 Forbidden error.
  - CORS Policy may be needed to allow cross-origin requests.
  - URL: `https://<bucket-name>.s3-website[.-]<aws-region>.amazonaws.com`

- **Temporary Access:**
  - Generate a pre-signed URL from CLI or SDK to provide temporary access to an S3 object (upload or download).
    - Example: `aws s3 presign s3://mybucket/myobject --expires-in 300`

- **Data Querying:**
  - **S3 Select** or **Glacier Select** can query subsets of data from S3 objects using SQL.
  - Supports CSV, JSON, or Apache Parquet. GZIP & BZIP2 compression is supported with CSV or JSON formats with server-side encryption.
  - Use Range HTTP Header in a GET Request for Byte Range Fetch.

- **Event Notifications:**
  - Create S3 event notifications to push events (e.g., `s3:ObjectCreated:*`) to SNS topics, SQS queues, or execute Lambda functions.
  - Single notification might be received for two writes to a non-versioned object simultaneously; enable versioning to ensure all notifications are received.

- **Replication & Logging:**
  - **Cross-Region Replication:** Asynchronous replication of objects across buckets in another region. Must enable versioning on both source and destination sides. Only new S3 objects are replicated after enabling.
  - **Server Access Logging:** Logs object-level fields (object-size, total time, turnaround time, HTTP referrer). Not available with CloudTrail.
  - Use VPC S3 gateway endpoint for accessing S3 bucket within AWS VPC to reduce overall data transfer cost.

- **Performance Optimization:**
  - **S3 Transfer Acceleration:** Faster transfer and high throughput for S3 bucket uploads.
  - Create a CloudFront distribution with OAI pointing to S3 for faster-cached content delivery (mainly reads).
  - Restrict access to S3 bucket through CloudFront only using Origin Access Identity (OAI).

- **Storage Class Types:**
  - **Standard:** Costly choice for very high availability, high durability, and fast retrieval.
  - **Intelligent Tiering:** Uses ML to analyze object usage and move to the appropriate cost-effective storage class automatically.
  - **Standard-IA:** Cost-effective for infrequent access files which cannot be recreated.
  - **One-Zone IA:** Cost-effective for infrequent access files which can be recreated.
  - **Glacier:** Cheaper choice for archiving data. Must purchase Provisioned capacity for guaranteed Expedite retrievals.
  - **Glacier Deep Archive:** Cheapest for long-term storage of large amounts of data for compliance.

- **Storage Class Details:**
  - **S3 Standard (General Purpose):**
    - Durability: 11 9’s
    - Availability: 99.99%
    - AZ: ≥3
    - Retrieval Time: milliseconds
    - Retrieval Fee: N/A
  - **S3 Intelligent Tiering:**
    - Durability: 11 9’s
    - Availability: 99.9%
    - AZ: ≥3
    - Minimum Storage: 30 days
    - Retrieval Time: milliseconds
    - Retrieval Fee: N/A
  - **S3 Standard-IA (Infrequent Access):**
    - Durability: 11 9’s
    - Availability: 99.9%
    - AZ: ≥3
    - Minimum Storage: 30 days
    - Retrieval Time: milliseconds
    - Retrieval Fee: per GB
  - **S3 One Zone-IA (Infrequent Access):**
    - Durability: 11 9’s
    - Availability: 99.5%
    - AZ: 1
    - Minimum Storage: 30 days
    - Retrieval Time: milliseconds
    - Retrieval Fee: per GB
  - **S3 Glacier:**
    - Durability: 11 9’s
    - Availability: 99.99%
    - AZ: ≥3
    - Minimum Storage: 90 days
    - Retrieval Time: Expedite (1-5 mins), Standard (3-5 hrs), Bulk (5-12 hrs)
    - Retrieval Fee: per GB
  - **S3 Glacier Deep Archive:**
    - Durability: 11 9’s
    - Availability: 99.99%
    - AZ: ≥3
    - Minimum Storage: 180 days
    - Retrieval Time: Standard (12 hrs), Bulk (48 hrs)
    - Retrieval Fee: per GB


##### <span style="color:blue">**S3 Storage Class Types**</span>

| **Storage Class**        | **Durability** | **Availability** | **AZ** | **Min. Storage** | **Retrieval Time**                       | **Retrieval Fee**   |
|--------------------------|----------------|------------------|--------|------------------|-----------------------------------------|---------------------|
| **S3 Standard** (General Purpose)   | 11 9’s         | 99.99%           | ≥3     | N/A              | milliseconds                             | N/A                 |
| **S3 Intelligent Tiering** | 11 9’s         | 99.9%            | ≥3     | 30 days          | milliseconds                             | N/A                 |
| **S3 Standard-IA** (Infrequent Access) | 11 9’s         | 99.9%            | ≥3     | 30 days          | milliseconds                             | per GB              |
| **S3 One Zone-IA** (Infrequent Access) | 11 9’s         | 99.5%            | 1      | 30 days          | milliseconds                             | per GB              |
| **S3 Glacier**           | 11 9’s         | 99.99%           | ≥3     | 90 days          | Expedite (1-5 mins), Standard (3-5 hrs), Bulk (5-12 hrs) | per GB              |
| **S3 Glacier Deep Archive** | 11 9’s         | 99.99%           | ≥3     | 180 days         | Standard (12 hrs), Bulk (48 hrs)        | per GB              |



- **Lifecycle Rules:**
  - Set up S3 Lifecycle Rules to transition current (or previous version) objects to cheaper storage classes or delete objects after certain days.
    - Example: Transition from S3 Standard to S3 Standard-IA or One Zone-IA can only be done after 30 days.
    - Immediate transition from S3 Standard to S3 Intelligent Tiering, Glacier, or Glacier Deep Archive is allowed.
    - Setup lifecycle rule to abort multipart upload if not completed within a certain period, which auto-deletes parts associated with multipart upload.

- **Encryption:**
  - **Encryption in Transit:** Achieved via SSL/TLS between client and S3.
  - **Encryption at Rest - Server Side Encryption (SSE):**
    - **SSE-S3:** AWS S3 managed keys, AES-256 algorithm.
    - **SSE-KMS:** Envelope encryption using AWS KMS managed keys.
    - **SSE-C:** Customer provides and manages keys; HTTPS is mandatory.
  - **Encryption at Rest - Client Side Encryption:** Client encrypts and decrypts data before sending and after receiving from S3.
    - For PCI-DSS or HIPAA compliance, use SSE-C and Client Side Encryption.

- **Data Consistency:**
  - S3 provides strong read-after-write consistency for PUTs and DELETEs of objects. PUTs apply to both new objects and overwrites of existing objects.
  - Updates to a single key are atomic, ensuring either old or new data is retrieved but not partial or corrupt data.

#### Amazon S3 Notifications Overview

---

##### **Enabling Notifications**
- **Configuration**: Add a notification configuration to specify events and destinations.
- **Storage**: Configuration is stored in the notification subresource associated with a bucket.
- **API**: Amazon S3 provides an API to manage the notification subresource.

##### **Event Notification Delivery**
- **Typical Delivery**: Events are typically delivered in seconds but can sometimes take a minute or longer.
- **Concurrency Handling**: If two writes are made to a single non-versioned object simultaneously, only one event notification may be sent.
- **Ensuring Event Notification**: Enable versioning on your bucket to ensure an event notification is sent for every successful write.

##### **Supported Events**
1. **New object-created events**
2. **Object removal events**
3. **Restore object events**
4. **Reduced Redundancy Storage (RRS) object lost events**
5. **Replication events**

##### **Supported Destinations**
1. **Amazon Simple Notification Service (Amazon SNS) topic**
2. **Amazon Simple Queue Service (Amazon SQS) queue**
3. **AWS Lambda**

##### **Avoiding Execution Loops**
- **Potential Issue**: Notifications can cause an execution loop if they result in actions that trigger more notifications.
- **Solution**: 
  - Use two separate buckets to avoid loops.
  - Configure triggers to apply only to specific prefixes used for incoming objects.

---

###### Quick Notes

 
- **Notification Configuration**: Add and manage using Amazon S3 API.
- **Typical Event Delivery**: Seconds, occasionally longer.
- **Versioning**: Ensures notifications for every successful write.
- **Events**: Object creation, removal, restoration, RRS object loss, replication.
- **Destinations**: SNS, SQS, Lambda.
- **Execution Loop Prevention**: Use separate buckets or specific prefixes.

##### Setting Up Amazon S3 Event Notifications for Object Creation and Removal

---

#### **Objectives**
- **Track new objects added to the bucket.**
- **Track objects removed from the bucket.**
- **Track permanently deleted versioned objects.**

> **Note:** `s3:ObjectRemoved:DeleteMarkerCreated` is triggered only when a delete marker is created for a versioned object, not when an object is deleted or a versioned object is permanently deleted.

---

### **Steps to Configure S3 Event Notifications**

1. **Create an Amazon SNS Topic**

    ```bash
    aws sns create-topic --name my-s3-events-topic
    ```

2. **Create an Amazon SQS Queue**

    ```bash
    aws sqs create-queue --queue-name my-s3-events-queue
    ```

3. **Add SNS Subscription to SQS Queue**

    ```bash
    aws sns subscribe --topic-arn arn:aws:sns:<span style="color: blue;">region</span>:<span style="color: blue;">account-id</span>:my-s3-events-topic --protocol sqs --notification-endpoint arn:aws:sqs:<span style="color: blue;">region</span>:<span style="color: blue;">account-id</span>:my-s3-events-queue
    ```

4. **Add S3 Event Notification Configuration**

    ```json
    {
      "NotificationConfiguration": {
        "TopicConfigurations": [
          {
            "Id": "NewObjectCreatedEvents",
            "TopicArn": "arn:aws:sns:<span style="color: blue;">region</span>:<span style="color: blue;">account-id</span>:my-s3-events-topic",
            "Events": [
              "s3:ObjectCreated:*"
            ]
          }
        ],
        "QueueConfigurations": [
          {
            "Id": "ObjectRemovedEvents",
            "QueueArn": "arn:aws:sqs:<span style="color: blue;">region</span>:<span style="color: blue;">account-id</span>:my-s3-events-queue",
            "Events": [
              "s3:ObjectRemoved:Delete"
            ]
          }
        ]
      }
    }
    ```

    **Add the above configuration using the AWS CLI:**

    ```bash
    aws s3api put-bucket-notification-configuration --bucket my-bucket --notification-configuration file://notification-config.json
    ```

---

##### **Event Types Tracked**
- **s3:ObjectCreated:\***
    - Tracks all object creation events.
- **s3:ObjectRemoved:Delete**
    - Tracks object removal events, including permanent deletions of versioned objects.

---

###### **Summary**
- **New SNS Topic**: `my-s3-events-topic`
- **New SQS Queue**: `my-s3-events-queue`
- **Notification Configuration**: Tracks `s3:ObjectCreated:*` and `s3:ObjectRemoved:Delete` events, publishing to both SNS and SQS.

 

---
### Amazon S3 Glacier Retrieval Options

#### **Expedited Retrievals** ![Blue](https://via.placeholder.com/15/0000FF/000000?text=+)
- **Purpose:** Quickly access data for urgent requests stored in the S3 Glacier Flexible Retrieval storage class or S3 Intelligent-Tiering Archive Access tier.
- **Typical Access Time:** 1–5 minutes for archives <250 MB.
- **Provisioned Capacity:** Ensures retrieval capacity for expedited requests.
- **Usage:** Use the **Tier** request element in the RestoreObject REST API, AWS CLI, or AWS SDKs.

#### **Standard Retrievals** ![Green](https://via.placeholder.com/15/008000/000000?text=+)
- **Purpose:** Access any of your archives within several hours.
- **Typical Access Time:** 3–5 hours.
- **Default Option:** For retrieval requests that do not specify a retrieval option.
- **Usage:** Use the **Tier** request element in the RestoreObject REST API, AWS CLI, or AWS SDKs.

#### **Bulk Retrievals** ![Red](https://via.placeholder.com/15/FF0000/000000?text=+)
- **Purpose:** Retrieve large amounts of data inexpensively.
- **Typical Access Time:** 5–12 hours.
- **Lowest Cost:** Ideal for retrieving petabytes of data.
- **Usage:** Use the **Tier** request element in the RestoreObject REST API, AWS CLI, or AWS SDKs.

#### **Provisioned Capacity** ![Purple](https://via.placeholder.com/15/800080/000000?text=+)
- **Purpose:** Ensures retrieval capacity for expedited retrievals when needed.
- **Details:** Each unit provides at least three expedited retrievals every 5 minutes and up to 150 MB/s of retrieval throughput.
- **Recommendation:** Purchase if your workload requires highly reliable and predictable access to a subset of your data in minutes.
- **Purchase Method:** S3 Glacier console, Purchase Provisioned Capacity (POST provisioned-capacity) REST API, AWS SDKs, AWS CLI.
- **Duration:** A provisioned capacity unit lasts for one month from the date and time of purchase.
- **Pricing:** Refer to [Amazon S3 Glacier Pricing](https://aws.amazon.com/s3/pricing/).

### **Retrieval Options Summary** ![Orange](https://via.placeholder.com/15/FFA500/000000?text=+)

| **Service**              | **Expedited**                | **Standard**               | **Bulk**                   |
|--------------------------|------------------------------|----------------------------|----------------------------|
| **Amazon S3 Glacier**    | 1–5 minutes                  | 3–5 hours                  | 5–12 hours                 |

### **Key Points** ![Orange](https://via.placeholder.com/15/FFA500/000000?text=+)
- **Expedited:** Fast retrievals (1–5 minutes), especially for archives <250 MB. Use provisioned capacity for guaranteed access.
- **Standard:** Default retrieval option (3–5 hours) for general use.
- **Bulk:** Cost-effective retrieval for large datasets (5–12 hours).
- **Provisioned Capacity:** Ensures expedited retrieval capacity is available when needed; each unit provides three expedited retrievals every 5 minutes and up to 150 MB/s of throughput.

### **Purchasing Provisioned Capacity** ![Pink](https://via.placeholder.com/15/FF1493/000000?text=+)
- **Methods:** S3 Glacier console, REST API, AWS SDKs, AWS CLI.
- **Benefits:** Highly reliable and predictable access to a subset of data in minutes.
- **Duration:** Lasts for one month from the date and time of purchase.

### **Range Retrievals** ![Teal](https://via.placeholder.com/15/008080/000000?text=+)
- **Purpose:** Manage data downloads and retrieve specific parts of a large archive.
- **Requirement:** Must provide a range that is megabyte aligned.
- **Checksum:** Ensure data integrity using tree-hash aligned range.

### **Comparative Table of Retrieval Options** ![Grey](https://via.placeholder.com/15/808080/000000?text=+)

| **Aspect**                          | **Expedited**                   | **Standard**                    | **Bulk**                       |
|-------------------------------------|---------------------------------|---------------------------------|--------------------------------|
| **Access Time**                     | 1–5 minutes                     | 3–5 hours                       | 5–12 hours                     |
| **Typical Use Case**                | Urgent data access              | General-purpose retrievals      | Large-scale, cost-effective retrievals |
| **Cost**                            | Higher                          | Medium                          | Lowest                         |
| **Provisioned Capacity**            | Available, ensures fast access  | Not required                    | Not required                   |
| **Usage**                           | High-urgency scenarios          | Regular access needs            | Large data retrieval at low cost |
| **Throughput with Provisioned Capacity** | Up to 150 MB/s                   | N/A                              | N/A                            |
.
 
 

- **AWS Athena:**
  - Use AWS Athena (Serverless Query Engine) to perform analytics directly against S3 objects using SQL and save the analysis report in another S3 bucket.
  - Use Cases: One-time SQL queries on S3 objects, S3 access log analysis, serverless queries on S3, IoT data analytics in S3, etc.


### <span style="color:blue">Instance Store</span>

- **Description:** Temporary block-based storage physically attached to an EC2 instance, also known as ephemeral storage.
- **Characteristics:**
  - **Attachment:** Can only be attached at launch time; not dynamically resizable.
  - **Performance:** Very low-latency and high random I/O performance.
  - **Persistence:** Data persists on instance reboot, but not on stop or termination.

### <span style="color:blue">EBS (Elastic Block Store)</span>

- **Description:** Block-based storage for EC2 instances, similar to a USB stick.
- **Characteristics:**
  - **Attachment:** Can be attached to only one EC2 instance at a time; can be detached and reattached to another instance in the same AZ.
  - **Persistence:** Data persists after detaching from EC2.
  - **Snapshots:** Point-in-time backups of EBS volumes; can be copied across AWS regions but not directly across AZs.

- **Encryption Facts:**
  - **Data at Rest:** Encrypted inside the volume.
  - **In Flight:** Encrypted between volume and EC2 instance.
  - **Snapshots:** Automatically encrypted; new volumes created from encrypted snapshots are also encrypted.
  - **Unencrypted Snapshots:** Can be encrypted at creation.

- **Volume Types:**
  | **Volume Type**               | **Description**                             | **Usage**                                    |
  |-------------------------------|---------------------------------------------|----------------------------------------------|
  | **General Purpose SSD (gp2/gp3)** | Max 16,000 IOPS                            | Boot volumes, dev environment, virtual desktops |
  | **Provisioned IOPS SSD (io1/io2)** | 16,000 - 64,000 IOPS, EBS Multi-Attach    | Critical business applications, large SQL/NoSQL databases |
  | **Throughput Optimized HDD (st1)** | Low-cost, throughput intensive             | Big Data, data warehouses, log processing   |
  | **Cold HDD (sc1)**            | Lowest-cost, infrequently accessed          | Large data with lowest cost                 |

- **RAID Configurations:**
  | **RAID Level** | **Description**                                                                 |
  |----------------|---------------------------------------------------------------------------------|
  | **RAID 0**     | Increases performance. Example: two 500GB volumes with 4000 IOPS become 1000GB with 8000 IOPS and 1000 Mbps throughput. |
  | **RAID 1**     | Increases fault tolerance. Example: two 500GB volumes with 4000 IOPS become 500GB with 4000 IOPS and 500 Mbps throughput. |

### <span style="color:blue">EFS (Elastic File System)</span>

- **Description:** POSIX-compliant file-based storage with strong read-after-write consistency and file locking.
- **Characteristics:**
  - **Scalability:** Automatically scales from gigabytes to petabytes.
  - **Availability:** Stores data across multiple AZs.
  - **Performance Modes:**
    | **Performance Mode** | **Description**                                                    | **Use Case**                             |
    |----------------------|--------------------------------------------------------------------|------------------------------------------|
    | **General Purpose**  | Low-latency file operations                                        | Content management, web serving          |
    | **Max I/O**          | High aggregated throughput and IOPS with slightly higher latency  | Big data analytics, media processing     |

### <span style="color:blue">FSx for Windows</span>

- **Description:** Windows-based file system supporting SMB protocol & Windows NTFS.
- **Characteristics:**
  - **Integration:** Supports Microsoft AD integration, ACLs, user quotas.

### <span style="color:blue">FSx for Lustre</span>

- **Description:** POSIX-compliant parallel file system optimized for high-performance computing.
- **Characteristics:**
  - **Performance:** Provides sub-millisecond latencies, hundreds of gigabytes per second of throughput, and millions of IOPS.
  - **Use Cases:** Machine learning, HPC, video processing, financial modeling, genome sequencing, EDA.
  - **Deployment Options:**
    | **Deployment Option** | **Description**                                       |
    |-----------------------|-------------------------------------------------------|
    | **Scratch File Systems** | For temporary storage and short-term processing.  |
    | **Persistent File Systems** | For high availability, persistent storage, and long-term processing. |

### <span style="color:blue">Comparison of Storage Options</span>

| **Feature**                  | **Instance Store**                                  | **EBS (Elastic Block Store)**                      | **EFS (Elastic File System)**                                | **FSx for Windows**                                  | **FSx for Lustre**                                  |
|------------------------------|------------------------------------------------------|----------------------------------------------------|--------------------------------------------------------------|-----------------------------------------------------|-----------------------------------------------------|
| **Type**                     | Block-based (Ephemeral Storage)                     | Block-based                                       | File-based (POSIX-compliant)                                | File-based (SMB protocol, Windows NTFS)           | File-based (POSIX-compliant parallel)              |
| **Attachment**               | At instance launch only                             | Dynamically attach/detach within the same AZ       | Mountable by thousands of EC2 instances                     | Attachable to Windows-based instances               | Attachable to Linux-based instances                 |
| **Persistence**              | Data persists on reboot, but not on stop/termination | Data persists after detaching from EC2             | Data persists across multiple AZs                          | Data persists and integrates with Microsoft AD      | Data persists, can integrate with S3               |
| **Performance**              | Low-latency, high random I/O                        | Varied based on volume type (SSD/HDD)               | High scalability, performance depends on mode               | Optimized for Windows applications                  | High performance with sub-millisecond latency       |
| **Volume Types/Performance** | -                                                    | General Purpose SSD, Provisioned IOPS SSD, Throughput Optimized HDD, Cold HDD | General Purpose, Max I/O                                | General Purpose, Optimized for Windows              | Scratch (temporary), Persistent (long-term)        |
| **RAID Configurations**      | Not applicable                                      | RAID 0 (performance), RAID 1 (fault tolerance)    | Not applicable                                              | Not applicable                                        | Not applicable                                       |
| **Snapshot/Backup**          | Not applicable                                      | Snapshots for backups; cross-region copy possible | Not applicable                                              | Not applicable                                        | Not applicable                                       |
| **Encryption**               | Not supported                                       | Supported (SSE-S3, SSE-KMS, SSE-C)                 | Supported (integrated with AWS KMS)                         | Supported (integrated with AWS KMS)                  | Supported (integrated with AWS KMS)                 |
| **Typical Use Cases**        | Temporary storage for high-performance applications | Boot volumes, database storage, application data   | File sharing, content management, web serving               | Windows applications, file sharing                  | High-performance computing, big data, media processing |

