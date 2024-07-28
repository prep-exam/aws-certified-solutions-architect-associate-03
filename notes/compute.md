Here's the information formatted in Markdown with color:

---

### <span style="color:green">EC2 (Elastic Compute Cloud)</span>
- **Description:** Infrastructure as a Service (IaaS) - virtual machine on the cloud.
- **Nitro vs. Non-Nitro Instances:** Nitro-based EC2 instances can achieve up to 64,000 EBS IOPS, while non-Nitro instances are limited to 32,000 EBS IOPS.
- **Public IP Management:** When you restart an EC2 instance, its public IP can change. Use Elastic IP to assign a fixed public IPv4 to your EC2 instance. By default, AWS accounts are limited to five Elastic IP addresses per Region.
- **Metadata Access:** Access EC2 instance metadata such as private & public IP from `http://169.254.169.254/latest/meta-data` and user-defined data from `http://169.254.169.254/latest/user-data`.
- **Cost Reduction:** Place all EC2 instances in the same Availability Zone (AZ) to reduce data transfer costs.
- **Hibernate:** EC2 Hibernate saves the contents of instance memory (RAM) to the Amazon EBS root volume. When the instance restarts, the RAM contents are reloaded, restoring the instance to its last running state. Hibernation must be enabled and meet certain prerequisites.
- **VM Import/Export:** Import virtual machine images and convert them to Amazon EC2 AMIs to launch EC2 instances.

---

### <span style="color:green">EC2 Instance Types</span>
| **Instance Class** | **Usage Type**           | **Usage Example**                                          |
|--------------------|--------------------------|------------------------------------------------------------|
| T, M               | General Purpose          | Web Server, Code Repo, Microservice, Small Database, Virtual Desktop, Dev Environment |
| C                  | Compute Optimized        | High Performance Computing (HPC), Batch Processing, Gaming Server, Scientific Modelling, CPU-based Machine Learning |
| R, X, Z            | Memory Optimized         | In-memory Cache, High Performance Database, Real-time Big Data Analytics |
| F, G, P            | Accelerated Computing    | High GPU, Graphics Intensive Applications, Machine Learning, Speech Recognition |
| D, H, I            | Storage Optimized        | EC2 Instance Storage, High I/O Performance, HDFS, MapReduce File Systems, Spark, Hadoop, Redshift, Kafka, Elasticsearch |

---

### <span style="color:green">EC2 Launch Types</span>
- **On-Demand:** Pay-as-you-go, per hour, costly.
- **Reserved:**
  - **Standard:** Unused instances can be sold in the AWS Reserved Instance Marketplace.
  - **Convertible:** Can be exchanged for another Convertible Reserved Instance with different instance attributes.
  - **Scheduled Reserved Instances:** Reserve capacity for a specified schedule (daily, weekly, monthly) for a one-year term.
- **Spot Instances:** Up to 90% discount, suitable for applications with flexible timing. Spot blocks are not interrupted due to changes in Spot price.
- **Spot Fleet:** Collection of Spot Instances and optionally On-Demand Instances to meet the specified target capacity.
- **Dedicated Instance:** Runs on dedicated hardware providing physical isolation (single-tenant).
- **Dedicated Hosts:** Instances run on a dedicated physical server, allowing visibility of instance placement and use of existing server-bound software licenses.
- **Limits:** Default limit of 20 Reserved Instances, 1,152 vCPU On-Demand standard instances, and 1,440 vCPU Spot Instances. Limits can be increased by submitting an EC2 limit increase request.

---

### <span style="color:green">EC2 Enhanced Networking</span>
- **Elastic Network Interface (ENI):** Virtual network card attached to EC2 instances in the same AZ. Includes primary and secondary private IPs, Elastic IP, public IPv4, IPv6, security groups, MAC address, and source/destination check flag. Secondary ENIs can be detached and attached to standby instances.
- **Elastic Network Adapter (ENA):** Provides up to 100 Gbps network speed for C4, D2, and M4 instances.
- **Elastic Fabric Adapter (EFA):** ENA with additional OS-bypass functionality for high-performance computing and machine learning applications, providing very high performance and low latency. Supported by M5, C5, R5, I3, G4, and metal instances.
- **Intel 82599 Virtual Function (VF) Interface:** Provides up to 10 Gbps network speed for C3, C4, D2, I2, M4, and R3 instances.

---

### <span style="color:green">EC2 Placement Groups Strategy</span>
- **Cluster:** Same AZ, same rack, low latency, high network performance, suitable for High-Performance Computing (HPC).
- **Spread:** Different AZs, distinct racks, high availability, critical applications. Limited to 7 instances per AZ per placement group.
- **Partition:** Same or different AZs, different racks or partitions, for distributed applications like Hadoop, Cassandra, Kafka. Up to 7 partitions per AZ.

---

Here's the information formatted in Markdown with color:

---

### <span style="color:blue">AMI (Amazon Machine Image)</span>
- **Description:** Customized image of an EC2 instance, including built-in OS, software, configurations, etc.
- **Usage:** Create an AMI from an EC2 instance and launch new EC2 instances from the AMI.
- **Region Specific:** AMIs are built for a specific region but can be copied across regions.

---

### <span style="color:blue">ELB (Elastic Load Balancing)</span>
- **Description:** AWS load balancer provides a static DNS name, e.g., `http://myalb-123456789.us-east-1.elb.amazonaws.com`.
- **Target Groups:** Routes requests to Target Groups, which can include EC2 instances, IP addresses, or Lambda functions.
- **Types of ELB:**
  - **Classic Load Balancer (CLB):** Older generation, supports HTTP, HTTPS, TCP.
  - **Application Load Balancer (ALB):** 
    - **Routing:** Based on hostname, request path, parameters, headers, source IP.
    - **Features:** Request tracing with `X-Amzn-Trace-Id` header, client IP and port in `X-Forwarded-For` and `X-Forwarded-Port` headers.
    - **Integration:** Works with AWS WAF for rate-limiting (throttle) rules to prevent DDoS attacks.
  - **Network Load Balancer (NLB):**
    - **Usage:** Handles volatile workloads and extreme low-latency.
    - **IP Management:** Provides static IP/Elastic IP per AZ.
    - **Target Registration:** Allows registering targets by IP address.
    - **Use Case:** Use NLB with Elastic IP in front of ALBs when there is a need for whitelisting ALB.
  - **Gateway Load Balancer:** Supports third-party appliances.

- **Stickiness:**
  - Works in CLB and ALB. Configured at Target Group level.
  - Not supported by NLB.

- **Supported Protocols:**
  - **Application Load Balancer:** HTTP, HTTPS, WebSocket
  - **Network Load Balancer:** TCP, UDP, TLS
  - **Gateway Load Balancer:** Third-party appliances
  - **Classic Load Balancer (old):** HTTP, HTTPS, TCP

---

### <span style="color:blue">ASG (Auto Scaling Group)</span>
- **Description:** Automatically scale EC2 instances based on scaling policies (e.g., CPU, network, custom metrics, or scheduled).
- **Capacity Settings:** Define minimum, maximum, and desired capacity. ASG maintains instances at the desired capacity if no policy is specified.
- **Launch Configuration vs. Launch Template:**
  - **Launch Configuration (Legacy):** Cannot be changed; requires creating a new configuration.
  - **Launch Template (Newer):** Allows multiple instance types and mixing Spot and On-Demand instances.
- **Scaling Policies:**
  - **Target Tracking Scaling:** Maintain average CPU utilization or request count. Uses the largest capacity if multiple policies are triggered simultaneously.
  - **Simple Scaling:** E.g., CloudWatch alarm CPUUtilization (>80%) - add 2 instances.
  - **Step Scaling:** E.g., CloudWatch alarm CPUUtilization (60%-80%) - add 1 instance, (>80%) - add 3 more, (30%-40%) - remove 1, (<30%) - remove 2 more.
  - **Scheduled Action:** E.g., Increase min capacity to 10 at 5 pm on Fridays.
- **Default Termination Policy:** Deletes instances in the AZ with the most number of instances and the oldest launch configuration. In case of a tie, the one closest to the next billing hour.
- **Cooldown Period:** Time to wait for previous scaling activity to take effect. Scaling activities during this period are ignored.
- **Health Check Grace Period:** Time to check the health status of a newly launched EC2 instance, giving it time to warm up.
- **Lifecycle Hooks:** Perform custom actions during:
  - **Scale-out:** E.g., Run scripts, install software, and send `complete-lifecycle-action` command.
  - **Scale-in:** E.g., Download logs, take snapshots before termination.

---

 
### <span style="color:blue">Lambda</span>

- **Type:** FaaS (Function as a Service), Serverless
- **Supported Languages:** Node.js, Python, Java, C#, Golang, Ruby, etc.

- **Limitations:**
  - **Execution Time:** Maximum of 900 seconds (15 minutes)
  - **Memory:** Minimum 128MB, up to 10GB with 1-MB increment
  - **Temporary Directory Size:** Maximum of 512MB
  - **Environment Variables Size:** Maximum of 4KB
  - **Code Size:**
    - **Compressed (.zip):** Maximum of 50MB
    - **Uncompressed:** Maximum of 250MB

- **Triggers:**
  - DynamoDB database triggers
  - S3 object events
  - EventBridge (CloudWatch Events) scheduled events
  - Messages received from SNS or SQS

- **IAM Role:** Assign IAM Role to give Lambda access to AWS resources (e.g., create EC2 snapshots, process images, store in S3).

- **Scaling:**
  - Auto scales in seconds to handle sudden traffic bursts
  - More cost-effective than EC2 (charged based on number of requests, execution time, and memory usage)

- **Additional Features:**
  - **Lambda@Edge:** Run code globally at CloudFront Edge locations
  - **Dead-Letter Queue (DLQ):** Optionally set up with SQS or SNS to handle unprocessed or failed requests
  - **Logging:** Enable and monitor execution logs in CloudWatch

---

### <span style="color:orange">AWS Fargate  </span>

**AWS Fargate** is a serverless compute engine for containers that works with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS). It simplifies the process of building applications by removing the need to provision and manage servers. Here are the key points to remember about AWS Fargate:

- **Serverless Compute Engine**: Works with ECS and EKS.
- **Focus on Applications**: Allows developers to focus on building applications without worrying about managing infrastructure.
- **Resource Specification and Payment**: Lets you specify and pay for resources per application.
- **Improved Security**: Enhances security through application isolation by design.
- **Automated Compute Allocation**: Allocates the right amount of compute, eliminating the need to choose instances and scale cluster capacity.
- **Cost Efficiency**: You only pay for the resources required to run your containers, avoiding over-provisioning and extra costs.
- **Ephemeral Storage**: By default, Fargate tasks are given a minimum of 20 GiB of free ephemeral storage, meeting the storage requirement in various scenarios.

#### <span style="color:darkgreen">AWS Fargate Features</span>

1. **Serverless Compute Engine**
   - Works with both ECS and EKS.
   - Removes the need to provision and manage servers.

2. **Resource Management**
   - Automatically allocates the right amount of compute.
   - Eliminates the need to choose instances and scale cluster capacity.

3. **Cost Efficiency**
   - Pay only for the resources required to run containers.
   - No over-provisioning and paying for additional servers.

4. **Application Isolation**
   - Enhances security through isolation by design.

5. **Storage**
   - Fargate tasks come with a minimum of 20 GiB of free ephemeral storage.

#### <span style="color:darkgreen">Usage and Benefits</span>

- **Focus on Building Applications**: Developers can concentrate on application development rather than managing infrastructure.
- **Predictable Costs**: Only pay for what you use, avoiding unexpected costs.
- **Improved Security**: Application isolation by design enhances overall security.
- **Scalability**: Automatically scales with application needs, providing the right amount of resources.

 