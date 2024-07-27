

### Amazon Kinesis Overview

Amazon Kinesis is a fully managed service designed to handle the collection, processing, and analysis of real-time streaming data in the cloud. This service is particularly valuable for applications that generate continuous data streams, such as IoT devices, gaming applications, vehicle tracking systems, and clickstream data from websites.

### Components of Amazon Kinesis

Amazon Kinesis is comprised of several key components, each with distinct functionalities:

1. **Kinesis Data Streams**
2. **Kinesis Data Firehose**
3. **Kinesis Data Analytics**
4. **Kinesis Video Streams**

#### Kinesis Data Streams

Kinesis Data Streams is responsible for capturing, processing, and storing data streams. It ensures that the data is available in real-time for various processing applications. 

- **Producers**: Data can be sent to Kinesis Data Streams using the Amazon Kinesis Agent, SDK, or Kinesis Producer Library (KPL).
- **Consumers**: The data from streams can be consumed by Kinesis Data Analytics, Kinesis Data Firehose, or applications using the Kinesis Consumer Library (KCL).
- **Data Retention**: The data retention period ranges from a default of 24 hours to a maximum of 365 days.
- **Order Maintenance**: Order is maintained at the shard (partition) level, ensuring that data is processed sequentially within each shard.

#### Kinesis Data Firehose

Kinesis Data Firehose is designed for loading data streams into various AWS data stores, including Amazon S3, Amazon Redshift, and Amazon Elasticsearch Service. It can also transform data using AWS Lambda functions and handle failed data by storing it in another S3 bucket.

#### Kinesis Data Analytics

Kinesis Data Analytics allows for real-time data analysis using SQL or Apache Flink. This component enables users to perform complex data processing and analysis on streaming data without needing to manage the underlying infrastructure.

#### Kinesis Video Streams

Kinesis Video Streams captures, processes, and stores video streams. This service is essential for applications requiring video data processing, such as security monitoring, video analytics, and media processing.

### Conclusion

Amazon Kinesis provides a comprehensive suite of services for managing real-time data streams. Its fully managed nature allows businesses to focus on extracting value from their streaming data without worrying about the underlying infrastructure. Whether you need to capture, process, store, or analyze streaming data, Amazon Kinesis offers the tools necessary to handle these tasks efficiently and effectively.


### Amazon EMR Overview

Amazon EMR (Elastic MapReduce) is a big data cloud platform designed for processing vast amounts of data using popular open-source tools. It is particularly suitable for running large-scale data transformation workloads, including Extract, Transform, Load (ETL) processes.

### Key Features and Tools

Amazon EMR integrates a variety of powerful open-source tools to handle different big data processing needs:

1. **Hadoop**: A framework that allows for the distributed processing of large data sets across clusters of computers.
2. **Apache Spark**: A unified analytics engine for large-scale data processing, known for its speed and ease of use.
3. **Apache Hive**: A data warehouse software that facilitates reading, writing, and managing large datasets residing in distributed storage using SQL.
4. **Apache HBase**: A distributed, scalable, big data store that provides real-time read/write access to large datasets.
5. **Apache Flink**: A stream processing framework that allows for real-time data processing.
6. **Apache Hudi**: A data lake framework that simplifies incremental data processing and pipeline development.
7. **Presto**: A distributed SQL query engine for running interactive analytic queries against data sources of all sizes.

### Use Cases

Amazon EMR is versatile and can be employed in various big data scenarios, including but not limited to:

- **Data Transformation Workloads (ETL)**: EMR can perform complex ETL operations, transforming raw data into actionable insights.
- **Log and Clickstream Analysis**: Analyzing clickstream data from Amazon S3 using Apache Spark and Hive can help businesses understand user behavior and deliver more effective ads.

### Example Use Case: Analyzing Clickstream Data

One common use case for Amazon EMR is the analysis of clickstream data to enhance advertising strategies. Here's how it works:

1. **Data Ingestion**: Clickstream data is collected from web and mobile applications and stored in Amazon S3.
2. **Data Processing**: Using Apache Spark and Apache Hive on Amazon EMR, the clickstream data is processed and analyzed. Spark provides fast, in-memory data processing, while Hive enables querying and managing large datasets with SQL.
3. **Insights Extraction**: The processed data is used to extract valuable insights about user behavior, preferences, and trends.
4. **Actionable Outcomes**: These insights help in crafting more targeted and effective advertising campaigns, ultimately improving user engagement and conversion rates.

### Conclusion

Amazon EMR provides a robust and scalable platform for big data processing, leveraging the power of widely-used open-source tools. Whether you're transforming data, analyzing clickstreams, or performing complex queries, EMR offers the flexibility and performance needed to handle large-scale data workloads efficiently.


### Amazon Neptune Overview

Amazon Neptune is a fully managed graph database service designed to build and run applications that work with highly connected datasets. It supports popular graph models, such as Property Graph and RDF (Resource Description Framework), and their respective query languages, Apache TinkerPop Gremlin and SPARQL.

#### Key Features
- **High Performance**: Neptune is optimized for fast query performance on large graph datasets.
- **Fully Managed**: Automated backups, software patching, and maintenance.
- **Scalable**: Easily scale read and write capacity to handle varying workloads.
- **Secure**: Encryption at rest, in transit, and integration with AWS Identity and Access Management (IAM).

#### Use Cases
- **High Relationship Data**: Ideal for applications that need to manage complex relationships, such as fraud detection and recommendation engines.
- **Social Networking Data**: Efficiently model and query social graphs, connecting users and content based on interactions and preferences.
- **Knowledge Graphs**: Manage vast amounts of interconnected information, such as Wikipedia data, to enhance search and data discovery capabilities.

### Example Use Case: Social Networking Data
1. **Data Modeling**: Users, posts, likes, comments, and relationships are modeled as nodes and edges.
2. **Query Execution**: Use Gremlin or SPARQL to traverse relationships and retrieve insights, such as finding mutual friends or trending posts.
3. **Real-Time Analysis**: Continuously update and query the graph to provide personalized recommendations and user interaction insights.

### Amazon Elasticsearch Service Overview

Amazon Elasticsearch Service (Amazon ES) is a fully managed service that makes it easy to deploy, secure, and operate Elasticsearch at scale. Elasticsearch is an open-source, distributed search and analytics engine.

#### Key Features
- **Managed Service**: Simplifies management tasks like hardware provisioning, software patching, and backups.
- **Scalable**: Automatically adjusts resources to handle data ingestion and query load.
- **Secure**: Supports VPC, IAM, and encryption for secure data access and transmission.

#### Integrations
- **Kinesis Data Firehose**: Seamlessly ingest streaming data into Amazon ES.
- **AWS IoT**: Ingest IoT data for real-time search and analytics.
- **CloudWatch Logs**: Monitor and troubleshoot applications by analyzing logs.

#### Use Cases
- **Search**: Provide fast and relevant search results across large datasets.
- **Indexing**: Index documents for quick retrieval and analysis.
- **Partial or Fuzzy Search**: Handle misspellings and variations in user queries to improve search accuracy.

### Example Use Case: Search and Indexing
1. **Data Ingestion**: Use Kinesis Data Firehose to stream data into Amazon ES.
2. **Indexing**: Automatically index data for efficient search and retrieval.
3. **Search Queries**: Perform partial or fuzzy searches to find relevant information even with incomplete or inaccurate queries.
4. **Real-Time Analytics**: Analyze and visualize data in real-time to gain actionable insights.

### Conclusion

Amazon Neptune and Amazon Elasticsearch Service offer powerful solutions for managing and analyzing complex datasets. Neptune excels in handling high-relationship and graph-based data, making it suitable for social networking and knowledge graphs. In contrast, Amazon Elasticsearch Service is designed for search, indexing, and real-time analytics, providing robust support for various applications requiring quick and accurate data retrieval.


## Migration

### AWS Migration Services Overview

AWS offers a comprehensive suite of migration services to facilitate the movement of data, applications, and databases from on-premises environments to the AWS cloud. Below is an overview of key AWS migration services, their features, and use cases.

### AWS Snow Family

The AWS Snow Family comprises a range of physical devices that help transfer large amounts of data from on-premises locations to Amazon S3, especially in scenarios with limited network connectivity.

#### Key Members and Features
1. **Snowcone**
   - **Storage**: 8TB
   - **RAM**: 4GB
   - **Migration Type**: Online & offline
   - **DataSync**: Yes
   - **Migration Size**: GBs and TBs
   - **Use Case**: Ideal for small-scale data migrations and edge computing.

2. **Snowball Edge Storage Optimized**
   - **Storage**: 80TB
   - **RAM**: 80GB
   - **Migration Type**: Offline
   - **DataSync**: No
   - **Migration Size**: Petabyte scale
   - **Use Case**: Large-scale data transfer and local storage.

3. **Snowball Edge Compute Optimized**
   - **Storage**: 42TB
   - **RAM**: 208GB
   - **Migration Type**: Offline
   - **DataSync**: No
   - **Migration Size**: Petabyte scale
   - **Use Case**: Compute-intensive workloads and large-scale data transfer.

4. **Snowmobile**
   - **Storage**: 100PB
   - **RAM**: N/A
   - **Migration Type**: Offline
   - **DataSync**: No
   - **Migration Size**: Exabyte scale
   - **Use Case**: Massive data migrations at an exabyte scale.

#### Migration Process
1. Install AWS OpsHub to manage and transfer files from on-premises machines to Snow devices.
2. Transfer data to an Amazon S3 bucket.
3. For long-term storage, use a lifecycle policy to move data to Amazon S3 Glacier. Direct migration to Glacier is not supported, but AWS DataSync can be used for this purpose.

### AWS Storage Gateway

AWS Storage Gateway enables hybrid cloud storage, allowing seamless integration between on-premises environments and AWS cloud storage.

#### Types and Use Cases
1. **File Gateway**
   - **Protocol**: NFS & SMB
   - **Backed by**: S3 -> S3-IA, S3 One Zone-IA
   - **Use Case**: Storing files as objects in S3 with local cache for low-latency access and user authentication using Active Directory.

2. **FSx File Gateway**
   - **Protocol**: SMB & NTFS
   - **Backed by**: FSx -> S3
   - **Use Case**: Integrating with Windows or Lustre file servers and Microsoft AD.

3. **Volume Gateway**
   - **Protocol**: iSCSI
   - **Backed by**: S3 -> EBS
   - **Use Case**: Providing block storage in S3 with EBS snapshot backups. Use Cached Volume for low-latency access and Stored Volume for scheduled backups.

4. **Tape Gateway**
   - **Protocol**: iSCSI VTL
   - **Backed by**: S3 -> S3 Glacier & Glacier Deep Archive
   - **Use Case**: Backup and archiving data in S3 using a tape-based process.

### AWS DataSync

AWS DataSync automates and accelerates the migration of large datasets from on-premises storage systems to AWS storage services.

#### Features
- **Protocol**: NFS & SMB
- **Destination**: S3, EFS, FSx for Windows, Snowcone
- **Direct Migration**: Supports direct migration to any S3 storage class, including Glacier and Glacier Deep Archive.
- **Private Network**: Use AWS Direct Connect for secure data migration to AWS services associated with VPC endpoints.

### AWS Backup

AWS Backup centralizes and automates the backup process across various AWS services.

#### Use Case
- Automate backups for EC2 instances, EBS volumes, EFS, RDS databases, DynamoDB tables, FSx for Lustre, FSx for Windows Server, and Storage Gateway volumes.
- Example: Automate RDS backups with a 90-day retention policy (exceeding the default 35-day limit).

### Database Migration Service (DMS)

AWS DMS facilitates database migration while minimizing downtime by keeping the source database operational during the migration process.

#### Features
- **Instance Requirement**: Requires an EC2 instance to run DMS.
- **Migration Types**: Supports both homogeneous (e.g., on-premises PostgreSQL to AWS RDS PostgreSQL) and heterogeneous (e.g., SQL Server to MySQL) migrations.
- **Schema Conversion**: Use AWS Schema Conversion Tool (SCT) for heterogeneous migrations.

### AWS Application Migration Service (MGN)

AWS MGN enables the migration of virtual machines from VMware vSphere, Microsoft Hyper-V, or Microsoft Azure to AWS.

#### Features
- **Replication Type**: Continuous, block-level replication.
- **Cutover Windows**: Enables cutover windows measured in minutes.
- **Legacy Service**: AWS Server Migration Service (SMS) offers snapshot-based replication with cutover windows measured in hours.

### Conclusion

AWS provides a robust set of services to facilitate various types of data and application migrations. From the physical transfer of large datasets with the Snow Family to seamless database migration with DMS, and continuous application migration with MGN, AWS offers tools designed to meet diverse migration needs efficiently and securely.

## Networking & Content Delivery


### Amazon VPC Overview

Amazon Virtual Private Cloud (VPC) enables you to create a logically isolated virtual network in the AWS cloud where you can launch AWS resources in a secure and scalable manner. Here's a detailed overview of VPC components and their functionalities:

### CIDR Block
CIDR (Classless Inter-Domain Routing) is a method for allocating IP addresses and IP routing.

#### Components
- **Base IP**: Example format (WW.XX.YY.ZZ)
- **Subnet Mask**: Ranges from /0 to /32

#### Examples
- **192.168.0.0/32**: \(2^{32-32} = 1\) single IP.
- **192.168.0.0/24**: \(2^{32-24} = 256\) IPs (192.168.0.0 to 192.168.0.255).
- **192.168.0.0/16**: \(2^{32-16} = 65,536\) IPs (192.168.0.0 to 192.168.255.255).
- **192.168.0.0/8**: \(2^{32-8} = 16,777,216\) IPs (192.0.0.0 to 192.255.255.255).
- **0.0.0.0/0**: \(2^{32-0} = All\) IPs (0.0.0.0 to 255.255.255.255).

### VPC (Virtual Private Cloud)
A VPC is a virtual network dedicated to your AWS account.

#### Key Features
- **Region Specific**: VPCs do not span across regions.
- **Default VPC**: Each region has a default VPC.
- **Limit**: Up to 5 VPCs per region.
- **CIDR Blocks**: Max 5 IPv4 CIDR blocks per VPC, minimum block size /28 (16 IPs) and maximum size /16 (65,536 IPs).
- **Secondary CIDR Blocks**: You can assign secondary CIDR ranges if the primary CIDR IPs are exhausted.
- **Private IP Ranges**: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16.
- **Non-Overlapping**: VPC CIDR blocks should not overlap with other VPCs in your AWS account.
- **DNS**: Enable DNS resolution and DNS hostnames; EC2 instances in the VPC will get domain names.

### VPC Peering
VPC peering connects two VPCs over a direct network route using private IP addresses.

#### Key Features
- **Behavior**: Instances in peered VPCs act as if they are on the same network.
- **CIDR**: No overlapping CIDR blocks allowed.
- **Non-Transitive**: VPC peering is not transitive (A-B and B-C does not imply A-C).
- **Route Tables**: Update route tables in both VPCs for communication.
- **Regions and Accounts**: Can peer VPCs in the same or different regions and AWS accounts.

### Subnets
A subnet is a range of IP addresses in your VPC.

#### Key Features
- **Association**: Each subnet is tied to one Availability Zone (AZ), one Route Table, and one Network ACL.
- **CIDR Block**: Assign one CIDR block per subnet within the VPC's CIDR range, ensuring no overlap with other subnets.
- **Reserved IPs**: AWS reserves the first 4 and the last IP in each subnet.
- **Public Subnets**: Enable auto-assign public IPv4 addresses for EC2 instances.
- **Multi-Tier Architecture**: For regions with 3 AZs, create 3 private and 3 public subnets for a highly available architecture. Public subnets host API gateways and ALBs, while private subnets host EC2 instances, Lambdas, and databases.


# AWS VPC Networking Components

## <span style="color:blue">Route Tables</span>

- **Definition**: A set of rules used to determine where network traffic is directed.
- **Rules**:
  - Each subnet in your VPC must be associated with a route table.
  - A subnet can only be associated with one route table at a time, but a route table can be associated with multiple subnets.
- **Types of Subnets**:
  - **Public Subnets**: Associated with a route table that has rules directing traffic to the <span style="color:green">Internet Gateway (IGW)</span>.
  - **Private Subnets**: Associated with a route table without rules for direct internet access. To access the internet, private subnets use a <span style="color:orange">NAT Gateway</span>.

## <span style="color:green">Internet Gateway (IGW)</span>

- **Definition**: Allows AWS instances in a public subnet to access the internet and be accessible from the internet.
- **Characteristics**:
  - Each IGW is associated with only one VPC.
  - Each VPC can have only one IGW (one-to-one mapping).

## <span style="color:orange">NAT Gateway</span>

- **Definition**: Provides internet access to instances in a private subnet but is not accessible from the internet.
- **Characteristics**:
  - Managed service that launches redundant instances within a selected Availability Zone (AZ) for high availability.
  - You must allocate an <span style="color:red">Elastic IP</span> to the NAT Gateway.
  - You should create a NAT Gateway in each AZ to ensure high availability.
  - NAT Gateways are automatically assigned a public IP address.
  - NAT Gateways work with IPv4.
  - NAT Gateways cannot be shared across VPCs.
  - NAT Gateways cannot be used as Bastions.

## <span style="color:purple">NAT Instances (Legacy)</span>

- **Definition**: Individual EC2 instances configured to function as NAT Gateways.
- **Characteristics**:
  - Requires manual management and failover handling.
  - Community AMIs are available to launch NAT Instances.
  - Works similarly to NAT Gateways but lacks some of their advanced features.
  - NAT Instances can be used as Bastions, unlike NAT Gateways.




## <span style="color:blue">Route Tables</span>

- **Definition**: A set of rules used to determine where network traffic is directed.
- **Rules**:
  - Each subnet in your VPC must be associated with a route table.
  - A subnet can only be associated with one route table at a time, but a route table can be associated with multiple subnets.
- **Types of Subnets**:
  - **Public Subnets**: Associated with a route table that has rules directing traffic to the <span style="color:green">Internet Gateway (IGW)</span>.
  - **Private Subnets**: Associated with a route table without rules for direct internet access. To access the internet, private subnets use a <span style="color:orange">NAT Gateway</span>.

## <span style="color:green">Internet Gateway (IGW)</span>

- **Definition**: Allows AWS instances in a public subnet to access the internet and be accessible from the internet.
- **Characteristics**:
  - Each IGW is associated with only one VPC.
  - Each VPC can have only one IGW (one-to-one mapping).

## <span style="color:orange">NAT Gateway</span>

- **Definition**: Provides internet access to instances in a private subnet but is not accessible from the internet.
- **Characteristics**:
  - Managed service that launches redundant instances within a selected Availability Zone (AZ) for high availability.
  - You must allocate an <span style="color:red">Elastic IP</span> to the NAT Gateway.
  - You should create a NAT Gateway in each AZ to ensure high availability.
  - NAT Gateways are automatically assigned a public IP address.
  - NAT Gateways work with IPv4.
  - NAT Gateways cannot be shared across VPCs.
  - NAT Gateways cannot be used as Bastions.

## <span style="color:purple">NAT Instances (Legacy)</span>

- **Definition**: Individual EC2 instances configured to function as NAT Gateways.
- **Characteristics**:
  - Requires manual management and failover handling.
  - Community AMIs are available to launch NAT Instances.
  - Works similarly to NAT Gateways but lacks some of their advanced features.
  - NAT Instances can be used as Bastions, unlike NAT Gateways.

## <span style="color:teal">Bastion Host</span>

- **Definition**: An individual small EC2 instance located in a public subnet.
- **Characteristics**:
  - Community AMIs exist to launch Bastion Hosts.
  - Used to access AWS instances in a private subnet with a private IPv4 address via SSH (port 22).

## <span style="color:darkblue">Egress-Only Internet Gateway</span>

- **Definition**: Provides outgoing internet access for IPv6 instances in a private subnet, similar to a NAT Gateway but for IPv6.
- **Characteristics**:
  - **Egress-Only**: Allows outgoing traffic only.
  - IPv6 addresses are public by default. This gateway allows IPv6 instances in a private subnet to access the internet without being accessible from the internet.



## <span style="color:blue">Route Tables</span>

- **Definition**: A set of rules used to determine where network traffic is directed.
- **Rules**:
  - Each subnet in your VPC must be associated with a route table.
  - A subnet can only be associated with one route table at a time, but a route table can be associated with multiple subnets.
- **Types of Subnets**:
  - **Public Subnets**: Associated with a route table that has rules directing traffic to the <span style="color:green">Internet Gateway (IGW)</span>.
  - **Private Subnets**: Associated with a route table without rules for direct internet access. To access the internet, private subnets use a <span style="color:orange">NAT Gateway</span>.

## <span style="color:green">Internet Gateway (IGW)</span>

- **Definition**: Allows AWS instances in a public subnet to access the internet and be accessible from the internet.
- **Characteristics**:
  - Each IGW is associated with only one VPC.
  - Each VPC can have only one IGW (one-to-one mapping).

## <span style="color:orange">NAT Gateway</span>

- **Definition**: Provides internet access to instances in a private subnet but is not accessible from the internet.
- **Characteristics**:
  - Managed service that launches redundant instances within a selected Availability Zone (AZ) for high availability.
  - You must allocate an <span style="color:red">Elastic IP</span> to the NAT Gateway.
  - You should create a NAT Gateway in each AZ to ensure high availability.
  - NAT Gateways are automatically assigned a public IP address.
  - NAT Gateways work with IPv4.
  - NAT Gateways cannot be shared across VPCs.
  - NAT Gateways cannot be used as Bastions.

## <span style="color:purple">NAT Instances (Legacy)</span>

- **Definition**: Individual EC2 instances configured to function as NAT Gateways.
- **Characteristics**:
  - Requires manual management and failover handling.
  - Community AMIs are available to launch NAT Instances.
  - Works similarly to NAT Gateways but lacks some of their advanced features.
  - NAT Instances can be used as Bastions, unlike NAT Gateways.

## <span style="color:teal">Bastion Host</span>

- **Definition**: An individual small EC2 instance located in a public subnet.
- **Characteristics**:
  - Community AMIs exist to launch Bastion Hosts.
  - Used to access AWS instances in a private subnet with a private IPv4 address via SSH (port 22).

## <span style="color:darkblue">Egress-Only Internet Gateway</span>

- **Definition**: Provides outgoing internet access for IPv6 instances in a private subnet, similar to a NAT Gateway but for IPv6.
- **Characteristics**:
  - **Egress-Only**: Allows outgoing traffic only.
  - IPv6 addresses are public by default. This gateway allows IPv6 instances in a private subnet to access the internet without being accessible from the internet.

## <span style="color:darkgreen">Network ACL (NACL)</span>

- **Definition**: Optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
- **Characteristics**:
  - VPCs come with a modifiable default NACL that allows all inbound and outbound traffic by default.
  - You can create custom NACLs. By default, each custom NACL denies all inbound and outbound traffic until you add rules.
  - Each subnet must be associated with only one NACL. If not specified, it auto-associates with the default NACL.
  - If you associate a subnet with a new NACL, the previous association is removed automatically.
  - Rules support both Allow and Deny rules.
  - **Stateless**: Requires explicit rules for both inbound and outbound traffic. Return traffic must be explicitly allowed by rules.
  - Rules are evaluated in number order, starting with the lowest numbered rule. For example, #100 ALLOW <IP> and #200 DENY <IP> means the IP is allowed based on the lower number rule.
  - Each NACL includes a default rule with the number *, which denies traffic if no numbered rule matches. This rule cannot be modified or removed.
  - It is recommended to create numbered rules in increments (e.g., increments of 10 or 100) to allow easy insertion of new rules later.
  - NACLs can block a single IP address, which cannot be done with Security Groups.

## <span style="color:blue">Security Group</span>

- **Definition**: Controls inbound and outbound traffic at the EC2 instance level.
- **Characteristics**:
  - Supports Allow rules only. All traffic is denied by default unless a rule specifically allows it.
  - **Stateful**: Return traffic is automatically allowed regardless of any rules.
  - When first created, a security group has no inbound rules (denies all incoming traffic) and one outbound rule that allows all outgoing traffic.
  - You can specify a source in the security group rule as an IP range, a specific IP (/32), or another security group.
  - One security group can be associated with multiple instances across multiple subnets.
  - One EC2 instance can be associated with multiple Security Groups, and rules are permissive (if one security group allows traffic, it is allowed regardless of other security groups).
  - All rules are evaluated before deciding whether to allow traffic.

# Comparison: Network ACLs (NACLs) vs. Security Groups

| Feature                          | <span style="color:darkgreen">Network ACL (NACL)</span>                             | <span style="color:blue">Security Group</span>                                |
|----------------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Purpose**                      | Firewall for controlling traffic in and out of one or more subnets.                  | Controls inbound and outbound traffic at the EC2 instance level.               |
| **Default Behavior**             | Default NACL allows all inbound and outbound traffic. Custom NACLs deny all traffic by default until rules are added. | Default Security Group denies all inbound traffic and allows all outbound traffic. |
| **Rules**                        | Supports both Allow and Deny rules.                                                   | Supports Allow rules only.                                                    |
| **Statefulness**                 | Stateless. Requires explicit rules for both inbound and outbound traffic. Return traffic must be explicitly allowed. | Stateful. Return traffic is automatically allowed regardless of rules.       |
| **Rule Evaluation**              | Rules are evaluated in number order (lowest to highest). Higher precedence is given to lower numbers. | All rules are evaluated before deciding whether to allow traffic.             |
| **Associations**                 | Each subnet must be associated with only one NACL. If a new NACL is associated, the previous association is removed. | One Security Group can be associated with multiple instances across multiple subnets. |
| **Rule Numbering**               | Rules are numbered from 1 to 32766. A default rule with a number * (asterisk) denies traffic if no other rule matches. | No rule numbering; all rules are evaluated for permissive access.              |
| **IP Address Blocking**           | Can block a single IP address, which cannot be done with Security Groups.              | Cannot block a single IP address; rules are based on IP ranges or other security groups. |
| **Application**                  | Applies to all instances within the associated subnet.                                | Applies to individual EC2 instances or groups of instances.                    |
| **Modification**                 | Custom NACLs require explicit rule configuration; default NACLs can be modified.     | Security Groups can be modified to add or remove rules.                        |




## <span style="color:darkred">Transit Gateway</span>

- **Definition**: Creates transitive VPC peer connections between thousands of VPCs.
- **Characteristics**:
  - **Hub-and-Spoke (Star) Connection**: Centralized routing model.
  - Supports IP Multicast (not supported by other AWS services).
  - Used as a gateway at the Amazon side in VPN connections, not at the customer side.
  - Can be attached to:
    - One or more VPCs
    - AWS Direct Connect gateway
    - VPN Connection
    - Peering connection to another Transit Gateway

## <span style="color:gray">VPC Flow Logs</span>

- **Definition**: Captures IP traffic information in and out of Network Interfaces within your VPC.
- **Characteristics**:
  - Can be enabled at the VPC, Subnet, or Network Interface level.
  - Logs can be delivered to S3 or CloudWatch Logs. You can query VPC flow logs using Athena on S3 or CloudWatch Logs Insights.
  - VPC Flow Logs include:
    - Log Version
    - AWS Account ID
    - Network Interface ID
    - Source IP address and port
    - Destination IP address and port
  - Contains source and destination IP addresses (not hostnames).
  - IPv6 addresses are all public. Private ranges still use IPv4. You cannot disable IPv4. Enabling IPv6 for a VPC and subnets means instances get both private IPv4 and public IPv6 addresses.

## <span style="color:darkorange">VPC Endpoints</span>

- **Definition**: Allow your VPC to connect to other AWS services privately within the AWS network.
- **Characteristics**:
  - Traffic between your VPC and other services never leaves the AWS network.
  - Eliminates the need for an Internet Gateway and NAT Gateway for instances in public and private subnets to access other AWS services through the public internet.
  - **Types**:
    - **Interface Endpoints**: Elastic Network Interfaces (ENIs) with a private IP address. Serve as entry points for traffic going to most AWS services. Provided by AWS PrivateLink with an hourly fee and per GB usage cost.
    - **Gateway Endpoints**: A gateway that is a target for a specific route in your route table, used for accessing supported AWS services. Currently supports only Amazon S3 and DynamoDB. Gateway endpoints are free.
  - For accessing S3 or DynamoDB in a different region privately, first establish VPC inter-region peering between VPCs in both regions, then use VPC Gateway Endpoint.
  - **AWS PrivateLink**: VPC interface endpoint service to expose a particular service to thousands of VPCs across accounts.
  - **AWS ClassicLink (Deprecated)**: Connects EC2-Classic instances privately to your VPC.

## <span style="color:darkblue">AWS VPN</span>

- **Definition**: Connects your remote network to Amazon VPC over the internet securely.
- **Components**:
  - **VPN Connection**: A secure connection between your on-premises equipment and Amazon VPCs.
  - **VPN Tunnel**: An encrypted link for data transfer between the customer network and AWS. Each VPN connection includes two VPN tunnels for high availability.
  - **Customer Gateway**: An AWS resource that provides information about your customer gateway device to AWS.
  - **Customer Gateway Device**: A physical device or software application on the customer side of the Site-to-Site VPN connection.
  - **Virtual Private Gateway**: The VPN concentrator on the Amazon side of the Site-to-Site VPN connection. You use a virtual private gateway or a transit gateway as the gateway for the Amazon side of the Site-to-Site VPN connection.
  - **Transit Gateway**: A transit hub used to interconnect your VPCs and on-premises networks. Can be used as the gateway for the Amazon side of the Site-to-Site VPN connection.  

# AWS VPC Networking Components

## <span style="color:blue">AWS Direct Connect</span>

- **Definition**: Establishes a dedicated private connection from on-premises locations to the AWS VPC network.
- **Features**:
  - Can access both public resources (e.g., S3) and private resources (e.g., EC2) on the same connection.
  - Provides network bandwidth ranging from 1 GB to 100 GB/s for fast data transfer from on-premises to the cloud.
  - Not an immediate solution; establishing a new connection takes a few days.

## <span style="color:darkblue">Comparison: AWS VPN vs. AWS Direct Connect</span>

| **Feature**                   | **AWS VPN**                     | **AWS Direct Connect**          |
|-------------------------------|---------------------------------|---------------------------------|
| **Connection Type**           | Over the internet                | Over a dedicated private connection |
| **Configuration Time**        | Configured in minutes            | Configured in days               |
| **Bandwidth**                 | Low to modest bandwidth          | High bandwidth (1 to 100 GB/s)   |

## <span style="color:green">Amazon API Gateway</span>

- **Definition**: Serverless service that allows you to create and manage APIs as a front door for back-end systems running on EC2, AWS Lambda, and other services.
- **API Gateway Types**:
  - **HTTP API**: Low latency and cost-effective API for modern web applications.
  - **WebSocket API**: Enables real-time, two-way communication between clients and servers.
  - **REST API**: Traditional API type with support for CRUD operations and HTTP methods.

- **Features**:
  - **Request Throttling**: Allows you to set throttle limits (default is 10,000 requests per second) to prevent overwhelming your backend. Uses the bucket-token algorithm where the burst size is the maximum bucket size.
    - **Example**: For a throttle limit of 10,000 req/s and a burst of 5,000 requests, if 8,000 requests come in the first millisecond, 5,000 are served immediately, and the remaining 3,000 are throttled over the next second.
  - **Caching**: Can be enabled to cache API responses, reducing the number of API calls and improving latency.

## <span style="color:purple">API Gateway Authentication</span>

- **IAM Policy**:
  - Used for authentication and authorization of AWS users.
  - Leverages Sig v4 to pass IAM credentials in the request header.

- **Lambda Authorizer** (formerly Custom Authorizer):
  - Uses a Lambda function for OAuth, SAML, or other third-party authentication mechanisms.

- **Cognito User Pools**:
  - Provides authentication only.
  - Allows management of your own user pool, which can be backed by providers like Facebook, Google, etc.

## <span style="color:orange">Amazon CloudFront</span>

- **Definition**: A Content Delivery Network (CDN) that uses AWS edge locations to cache and deliver content (e.g., images, videos) closer to end users for faster performance.

- **Caching Sources (Origins)**:
  - **S3 Bucket**:
    - **Origin Access Identity (OAI)**: Used to restrict access so that content in the S3 bucket is accessible only via CloudFront.
    - **S3 Bucket Policy**: Configured to allow access from CloudFront.
  - **EC2 or ALB**: Can be used as an origin if they are public and security groups allow access.

- **Features**:
  - **Geo Restriction (Geo-Blocking)**: Allows you to whitelist or blacklist countries that can access your content.
  - **Distribution Types**:
    - **Web Distribution**: For static and dynamic web content, and video streaming.
    - **RTMP Streaming Distribution**: For media files using the RTMP protocol (Adobe media server).
  - **Signed URLs and Signed Cookies**:
    - **Signed URL**: Used for granting access to a single file or RTMP streaming.
    - **Signed Cookie**: Used for granting access to multiple files.
  - **Integration with AWS WAF**: Provides web application firewall protection from layer 7 attacks.
  - **Cache Control**:
    - **TTL (Time-to-Live)**: Objects are removed from the cache upon expiry, with a default TTL of 24 hours.
    - **Invalidation**: Allows explicit removal of objects from the cache for web distributions, though this incurs a cost. Alternatively, you can use versioning or change object names to serve new content.

## <span style="color:darkblue">Summary of CloudFront Capabilities</span>

| **Feature**                   | **Details**                                           |
|-------------------------------|-------------------------------------------------------|
| **Content Delivery**          | Caches and delivers content via AWS edge locations   |
| **Origin Types**              | S3 bucket, EC2, ALB                                  |
| **Access Control**            | Origin Access Identity (OAI), S3 bucket policy       |
| **Geo Restriction**           | Whitelist or blacklist countries                     |
| **Distribution Types**        | Web Distribution, RTMP Streaming                      |
| **Access Control Mechanisms** | Signed URL (single file), Signed Cookie (multiple files) |
| **Integration**               | AWS WAF for layer 7 protection                        |
| **Cache Expiry**              | Default TTL of 24 hours; explicit invalidation available |


## <span style="color:blue">Overview</span>

Amazon Route 53 is a scalable and highly available Domain Name System (DNS) web service designed to provide DNS records and routing policies for your domains.

- **DNS Records**: Manage domain names and map them to IP addresses for various resources such as EC2 instances or load balancers.
- **Browser Caching**: Browsers cache the resolved IP from DNS for a duration specified by the TTL (Time-to-Live).

## <span style="color:darkblue">Domain Management</span>

- **Public IP Exposure**:
  - Use Route 53 to expose public IP addresses of EC2 instances or load balancers.
  
- **Domain Registrar Integration**:
  - **AWS Domains**:
    - Create a **Hosted Zone** in Route 53 for managing DNS records.
  - **Third-Party Registrars** (e.g., GoDaddy):
    - Update the NS (Name Server) records at the registrar to point to Route 53's name servers.

## <span style="color:green">Hosted Zones</span>

- **Public Hosted Zone**:
  - Manages DNS records for publicly accessible domains.
  
- **Private Hosted Zone**:
  - Used for creating internal (intranet) domain names that are accessible only within an Amazon VPC.
  - Allows you to add DNS records and routing policies for the internal domain.
  - Internal domains are accessible from EC2 instances and other resources within the VPC.

## <span style="color:purple">Key Points</span>

| **Feature**                  | **Details**                                           |
|------------------------------|-------------------------------------------------------|
| **DNS Management**           | Create and manage DNS records for domains            |
| **TTL (Time-to-Live)**       | Browsers cache resolved IPs based on TTL settings     |
| **Public IP Exposure**       | Route 53 exposes public IPs of resources             |
| **Domain Registrar Integration** | Update NS records at registrar to use Route 53    |
| **Hosted Zones**             | Public and Private Hosted Zones                      |
| **Private Hosted Zone**      | Internal domain management within an Amazon VPC      |


## <span style="color:darkred">Cost Considerations</span>

- **No Additional Cost**:
  - VPCs
  - Route Tables
  - NACLs
  - Internet Gateway
  - Security Groups
  - Subnets
  - VPC Peering

- **Cost Associated**:
  - NAT Gateway
  - VPC Endpoints
  - VPN Gateway
  - Customer Gateway