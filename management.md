## AWS Management & Governance

### <span style="color:blue">Amazon CloudWatch</span>

#### **Overview**
- **Purpose**: Collect and track metrics, monitor log files, and set alarms for AWS resources.
- **Resources Supported**: EC2, ALB, S3, Lambda, DynamoDB, RDS, etc.

#### **Features**
- **Metrics Collection**:
  - Default resolution: 1-minute intervals.
  - High-resolution metrics: Up to 1-second intervals.
- **Custom Metrics**:
  - EC2 instance metrics: CPU Utilization %, Network Utilization, Disk Read/Write.
  - Custom metrics: Memory Utilization, Disk Space Utilization, Swap Utilization (requires CloudWatch Logs Agent).
- **CloudWatch Dashboards**:
  - Visualize metrics and logs across different AWS accounts and regions.
- **Alarms**:
  - Configure alarms to monitor metrics and trigger actions (e.g., terminate or recover EC2 instances).
- **Events**:
  - Schedule tasks using CloudWatch Events (e.g., Cron jobs).
- **Permissions**:
  - Ensure AWS services have `log:CreateLogGroup`, `log:CreateLogStream`, and `log:PutLogEvents` permissions to write logs.

#### **Custom Metrics Setup**
- Install CloudWatch Logs Agent on EC2 instances to collect custom metrics and logs.
  
### <span style="color:green">AWS CloudTrail</span>

#### **Overview**
- **Purpose**: Provides audit and event history of actions taken by users, AWS services, CLI, or SDK across AWS infrastructure.
- **Default Setting**: Enabled by default for all regions.

#### **Features**
- **Log Delivery**:
  - CloudTrail logs can be sent to CloudWatch Logs or S3 buckets.
- **Use Case**:
  - Monitor and audit actions such as resource deletions, ensuring visibility into all activities across your AWS environment.

#### **Use Case Example**
- Check CloudTrail logs to verify if any resources were deleted without proper authorization or notification.

### <span style="color:purple">Summary Table</span>

| **Feature**          | **Amazon CloudWatch**                                    | **AWS CloudTrail**                                   |
|----------------------|----------------------------------------------------------|------------------------------------------------------|
| **Purpose**          | Collect metrics, monitor logs, and set alarms.           | Audit and event history of actions across AWS.      |
| **Default Setting**  | Metrics collected at 1-minute intervals by default.       | Enabled by default for all regions.                 |
| **Custom Metrics**   | Requires CloudWatch Logs Agent for non-default metrics.   | N/A                                                  |
| **Dashboard**        | Includes graphs from multiple accounts and regions.       | N/A                                                  |
| **Alarms**           | Can terminate or recover EC2 instances based on alarms.    | N/A                                                  |
| **Events**           | Schedule tasks using CloudWatch Events.                   | N/A                                                  |
| **Log Delivery**     | Logs and metrics can be visualized in dashboards.         | Logs can be sent to CloudWatch Logs or S3 buckets.   |
| **Permissions**      | Requires specific log permissions to write logs.          | N/A                                                  |

### AWS CloudFormation

##### <span style="color:blue">Overview</span>

- **Definition**: Infrastructure as Code (IaC) service that enables you to model, provision, and version your entire AWS infrastructure using a text file (JSON or YAML).
- **Purpose**: Create, update, or delete stacks of AWS resources using CloudFormation templates.

#### <span style="color:green">Components of CloudFormation Template</span>

1. **Resources**:
   - **Definition**: AWS resources defined in the template <span style="color:red">(mandatory)</span>.
   - **Example**: EC2 instances, S3 buckets, RDS databases.

2. **Parameters**:
   - **Definition**: Input values provided when creating the stack.
   - **Purpose**: Allow dynamic configuration of resources at stack creation time.
   - **Example**: Instance type, database name.

3. **Mappings**:
   - **Definition**: Static variables in the template.
   - **Purpose**: Define fixed values to be used for resource configuration.
   - **Example**: Region-specific AMI IDs.

4. **Outputs**:
   - **Definition**: Information returned after stack creation.
   - **Purpose**: Provide useful information about resources.
   - **Example**: Elastic IP address, ELB DNS name.

5. **Conditionals**:
   - **Definition**: List of conditions to control resource creation.
   - **Purpose**: Create resources only if certain conditions are met.
   - **Example**: Create resources only if a parameter is set to true.

6. **Metadata**:
   - **Definition**: Additional information about the template.
   - **Purpose**: Provide information used by tools or scripts.

7. **Template Helpers**:
   - **References**:
     - **Definition**: Allows you to refer to other resources in the template.
     - **Example**: `!Ref` to reference a resource.
   - **Functions**:
     - **Definition**: Built-in functions for dynamic values.
     - **Example**: `!GetAtt` to get an attribute from a resource.

#### <span style="color:orange">Advanced Features</span>

- **DependsOn Attribute**:
  - **Purpose**: Specifies the creation order of resources.
  - **Example**: Ensure an RDS instance is created before an EC2 instance.

- **DeletionPolicy Attribute**:
  - **Purpose**: Defines how AWS should handle resources upon stack deletion.
  - **Options**:
    - **Retain**: Preserve resources like S3 even after stack deletion.
    - **Snapshot**: Backup resources like RDS before deletion.

- **Bootstrap Scripts**:
  - **Purpose**: Install packages, files, and services on EC2 instances.
  - **Usage**: Describe in the template for automatic setup.

- **Automatic Rollback**:
  - **Definition**: Enabled by default.
  - **Purpose**: Deletes all resources created successfully up to the point where an error occurred.

- **StackSets**:
  - **Purpose**: Create, update, or delete CloudFormation stacks across multiple accounts, regions, or organizational units (OUs) in AWS.
  - **Usage**: Simplify management of stacks in a multi-account or multi-region environment.

##### <span style="color:purple">Cost</span>

- **Usage**: CloudFormation itself is free.
- **Charges**: Costs are incurred based on the underlying AWS resources defined in the template.

##### <span style="color:teal">Use Cases</span>

- **Environment Setup**: Set up the same infrastructure in different environments (e.g., SIT, UAT, PROD).
- **Cost Management**: Create resources on-demand (e.g., DEV resources during working hours and delete them afterward to lower costs).

## <span style="color:blue">Summary Table</span>

| **Feature**               | **Description**                                            |
|---------------------------|------------------------------------------------------------|
| **Definition**            | Infrastructure as Code (IaC) for AWS resources.            |
| **Template Components**   | Resources, Parameters, Mappings, Outputs, Conditionals, Metadata, Template Helpers. |
| **Advanced Features**     | DependsOn, DeletionPolicy, Bootstrap Scripts, Automatic Rollback, StackSets. |
| **Cost**                  | CloudFormation is free; charges apply to underlying resources. |
| **Use Cases**             | Environment setup, cost management, automated resource provisioning. |


# AWS Elastic Beanstalk

## <span style="color:blue">Overview</span>

- **Definition**: Platform as a Service (PaaS) that simplifies the deployment and management of applications.
- **Purpose**: Enables developers to deploy applications quickly without managing underlying resources.

## <span style="color:green">Features</span>

1. **Automatic Management**:
   - **Deployment**: Handles capacity provisioning, load balancing, auto-scaling, and application health monitoring.
   - **Resource Management**: Manages underlying resources such as EC2 instances, Auto Scaling Groups (ASG), Elastic Load Balancers (ELB), and RDS instances.

2. **Pre-configured Platforms**:
   - **Java**: Apache Tomcat.
   - **PHP/Python**: Apache HTTP Server.
   - **Node.js**: Nginx or Apache HTTP Server.
   - **Ruby**: Passenger or Puma.
   - **.NET**: Microsoft IIS 7.5.
   - **Docker**: Single and Multi Container Docker.

3. **Environment Tiers**:
   - **Web Server Environment**: Serves HTTP requests.
   - **Worker Environment**: Processes background tasks from an Amazon Simple Queue Service (Amazon SQS) queue.

4. **Custom AMI**:
   - **Support**: Allows the use of custom Amazon Machine Images (AMIs).

5. **Multiple Environments**:
   - **Support**: Enables development, staging, and production environments.

6. **Versioning**:
   - **Support**: Stores and tracks application versions over time, allowing easy rollback to previous versions.

## <span style="color:purple">Cost</span>

- **Service Cost**: AWS Elastic Beanstalk itself is free.
- **Resource Cost**: Charges are based on the resources it provisions, including EC2, Auto Scaling, ELB, and RDS.

## <span style="color:teal">Use Cases</span>

- **Rapid Deployment**: Quickly deploy and manage applications without managing infrastructure.
- **Version Control**: Maintain and rollback application versions easily.
- **Development Stages**: Use different environments for development, staging, and production.

## <span style="color:blue">Summary Table</span>

| **Feature**                  | **Description**                                            |
|------------------------------|------------------------------------------------------------|
| **Definition**               | Platform as a Service (PaaS) for application management.   |
| **Automatic Management**     | Capacity provisioning, load balancing, auto-scaling, health monitoring. |
| **Pre-configured Platforms** | Java (Tomcat), PHP/Python (Apache), Node.js (Nginx/Apache), Ruby (Passenger/Puma), .NET (IIS), Docker. |
| **Environment Tiers**        | Web server and worker environments.                       |
| **Custom AMI Support**       | Allows the use of custom Amazon Machine Images.            |
| **Multiple Environments**    | Supports development, staging, and production environments. |
| **Versioning**               | Tracks and manages application versions.                  |
| **Cost**                     | Free service; charges apply to underlying AWS resources.   |
| **Use Cases**                | Rapid deployment, version control, and development stages. |


# AWS ParallelCluster

## <span style="color:blue">Overview</span>

- **Definition**: A tool for deploying and managing High-Performance Computing (HPC) clusters on AWS using a simple text file.
- **Control**: Provides full control over the underlying resources.
- **Cost**: The service itself is free; you only pay for the AWS resources used.

## <span style="color:green">Features</span>

1. **Deployment**:
   - **Configuration**: Use a simple text file to configure and deploy HPC clusters.

2. **Elastic Fabric Adapter (EFA)**:
   - **Capabilities**: Enables OS-bypass for low-latency network communication.

3. **Cost Structure**:
   - **Service Cost**: Free.
   - **Resource Cost**: Charges apply based on the AWS resources used.

---

# AWS Step Functions (SF)

## <span style="color:blue">Overview</span>

- **Definition**: A service for building serverless visual workflows to orchestrate AWS Lambda functions.
- **Configuration**: Define workflows using declarative JSON.

## <span style="color:green">Features</span>

1. **Visual Workflow**:
   - **Creation**: Build and manage workflows that coordinate Lambda functions.

2. **Decider Program**:
   - **Purpose**: Separate activity steps from decision steps for better management.

3. **Serverless**:
   - **Integration**: Works seamlessly with AWS Lambda to handle serverless functions.

---

# AWS Simple Workflow Service (SWF)

## <span style="color:blue">Overview</span>

- **Definition**: A service that enables you to run code on EC2 instances with a focus on workflows.
- **Use Case**: Ideal for processes requiring external signals or interaction between child and parent processes.

## <span style="color:green">Features</span>

1. **Execution**:
   - **Code Location**: Runs on EC2 instances, not serverless.

2. **Use Cases**:
   - **When to Use**: Best for applications requiring external signals or value passing between processes.
   - **Alternative**: For new applications, consider using AWS Step Functions.

## <span style="color:teal">Summary Table</span>

| **Service**            | **Definition**                                    | **Features**                                             | **Cost Structure**                                      |
|------------------------|---------------------------------------------------|----------------------------------------------------------|--------------------------------------------------------|
| **AWS ParallelCluster** | Deploy and manage HPC clusters on AWS.            | Full resource control, Elastic Fabric Adapter (EFA) support. | Free service; pay for AWS resources used.             |
| **AWS Step Functions** | Build serverless workflows to orchestrate Lambda functions. | Visual workflow, decider program for step management.   | Cost depends on usage of Step Functions and Lambda.    |
| **AWS Simple Workflow Service (SWF)** | Run workflows on EC2 with external signals and process interactions. | External signal handling, process value passing.        | Pay for EC2 instances and other resources used.       |


# AWS Organizations

## <span style="color:blue">Overview</span>

- **Definition**: A global service used to manage multiple AWS accounts within a single organization.
- **Use Cases**: Managing accounts by department, cost center, or environment (e.g., dev, test, prod).

## <span style="color:green">Key Features</span>

1. **Centralized Management**:
   - **Accounts**: Manage multiple AWS accounts from a central organization.
   - **Billing**: Consolidate billing with a single payment method and benefit from aggregated usage across accounts.

2. **Organizational Units (OUs)**:
   - **Hierarchy**: OUs can contain other OUs, creating a hierarchical structure.
   - **Management**: Organize accounts into departments, cost centers, or environments.

3. **Service Control Policies (SCPs)**:
   - **Application**: SCPs can be applied at the OU or account level.
   - **Precedence**: Deny policies take precedence over Allow policies. If an account has an Allow policy at the account level but a Deny policy at the OU level, the effective policy is Deny.
   - **Master Account**: The master account retains full control, regardless of SCPs.

4. **Account Merging**:
   - **Process**:
     1. Remove all member accounts from the Firm_A organization.
     2. Delete the Firm_A organization.
     3. Invite the Firm_A master account to join the Firm_B organization as a member account.

5. **AWS Resource Access Manager (RAM)**:
   - **Resource Sharing**: Share resources like Transit Gateways, Subnets, AWS License Manager configurations, Route 53 resolver rules, etc., across accounts within the organization.
   - **Configuration**: Enable resource sharing at the AWS Organization level.

6. **AWS Control Tower Integration**:
   - **Purpose**: Helps set up and configure new AWS accounts with best practices.
   - **Landing Zone**: Provides a base setup called a landing zone for account provisioning.

## <span style="color:teal">Summary Table</span>

| **Feature**                   | **Description**                                                                                     |
|-------------------------------|-----------------------------------------------------------------------------------------------------|
| **Centralized Management**    | Manage multiple accounts and consolidate billing with a single payment method.                    |
| **Organizational Units (OUs)**| Create a hierarchical structure to manage accounts based on departments, cost centers, or environments. |
| **Service Control Policies (SCPs)** | Apply policies at the OU or account level; Deny takes precedence over Allow.                        |
| **Account Merging**           | Process to merge organizations by removing, deleting, and re-inviting accounts.                   |
| **AWS Resource Access Manager (RAM)** | Share resources across accounts within an organization; enable sharing at the organization level. |
| **AWS Control Tower Integration** | Configure new accounts with best practices and a landing zone.                                    |


# AWS OpsWorks

## <span style="color:blue">Overview</span>

- **Definition**: Managed instances of Chef and Puppet configuration management services for automating the configuration and operation of applications on AWS.
- **Purpose**: Automate server configuration, deployment, and management across EC2 instances using code.

## <span style="color:green">Key Features</span>

1. **Configuration as Code**:
   - **Chef and Puppet**: Use these tools to automate server configurations and management.

2. **OpsWorks Stack**:
   - **Modeling**: Define your application as a stack with various layers (e.g., load balancing, database, application server).
   - **Layers**: Each layer can contain different components or services of your application.

3. **Automated Management**:
   - **Deployment**: Streamline deployment processes using Chef/Puppet scripts.
   - **Configuration**: Manage server configurations efficiently.

## <span style="color:teal">Summary Table</span>

| **Feature**                  | **Description**                                                                  |
|------------------------------|----------------------------------------------------------------------------------|
| **Configuration as Code**    | Automate server configurations using Chef or Puppet.                            |
| **OpsWorks Stack**           | Model applications with different layers like load balancing and database.       |
| **Automated Management**     | Efficiently manage deployment and configuration processes.                       |

---

# AWS Glue

## <span style="color:blue">Overview</span>

- **Definition**: Serverless, fully managed ETL (Extract, Transform, Load) service for data processing.
- **Purpose**: Simplify the process of preparing and transforming data for analytics.

## <span style="color:green">Key Features</span>

1. **AWS Glue Crawler**:
   - **Function**: Scans data from sources like S3 or DynamoDB, determines the schema, and creates metadata tables in the AWS Glue Data Catalog.
   - **Data Sources**: Works with data from various sources to identify and catalog schema information.

2. **Classifiers**:
   - **Purpose**: Determine data schema for different formats including CSV, JSON, AVRO, XML, or databases.

## <span style="color:teal">Summary Table</span>

| **Feature**                  | **Description**                                                                                       |
|------------------------------|-------------------------------------------------------------------------------------------------------|
| **AWS Glue Crawler**         | Scans data sources to determine schema and create metadata tables in the Data Catalog.               |
| **Classifiers**              | Identify and catalog data schema for formats such as CSV, JSON, AVRO, XML, and databases.            |
| **Serverless ETL**           | Simplifies the ETL process without managing infrastructure.                                           |

 # AWS Containers

## <span style="color:blue">Amazon ECR (Elastic Container Registry)</span>

- **Definition**: Managed Docker container registry service.
- **Purpose**: Store, manage, and deploy Docker container images.

## <span style="color:blue">Amazon ECS (Elastic Container Service)</span>

### <span style="color:green">Overview</span>

- **Definition**: Container management service to run, stop, and manage Docker containers on a cluster.
- **Components**:
  - **ECS Task Definition**: Configuration for tasks and containers.
  - **ECS Service Definition**: Configuration for cluster, ELB, ASG, task definition, and task count.

### <span style="color:green">Key Features</span>

1. **ECS Task Definition**:
   - **Configuration**: Define tasks and containers, including Docker image, memory, port mappings, and health checks.
   - **IAM Roles**:
     - **ECS Task IAM Role**: Allows containers to access AWS services (e.g., S3, DynamoDB).
     - **Task Execution IAM Role**: `ecsTaskExecutionRole` for ECS Agent tasks, such as pulling images from ECR, making API calls, and publishing logs to CloudWatch.

2. **ECS Service Definition**:
   - **Configuration**: Includes cluster, ELB, ASG, task definition, and the number of tasks to run.
   - **Deployment**: Runs multiple similar tasks on EC2 instances, with each instance capable of running multiple tasks.

3. **Launch Types**:
   - **EC2 Launch Type**:
     - **Management**: You manage EC2 instances in the ECS cluster, including installing ECS Agent.
     - **Cost**: Cheaper, suitable for predictable, long-running tasks.
   - **Fargate Launch Type**:
     - **Management**: Fargate manages EC2 instances; you only manage and pay for container resources.
     - **Cost**: Costlier, suitable for variable, short-running tasks.

4. **ECS Agent**:
   - **Function**: Sends task and resource utilization information to ECS, starts and stops tasks as requested.

## <span style="color:blue">Amazon EKS (Elastic Kubernetes Service)</span>

- **Definition**: Managed Kubernetes service for deploying and managing Kubernetes clusters on AWS.
- **Purpose**: Simplifies the management of Kubernetes clusters, providing an integrated Kubernetes experience on AWS.

## <span style="color:teal">Summary Table</span>

| **Service**        | **Definition**                                      | **Purpose**                                              | **Key Features**                                                                                                       |
|--------------------|------------------------------------------------------|----------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| **ECR**            | Managed Docker registry service                     | Store, manage, and deploy Docker images                 | Managed registry, integration with ECS and EKS                                                                       |
| **ECS**            | Container management service                        | Manage Docker containers on a cluster                    | Task and Service Definitions, EC2 and Fargate Launch Types, ECS Agent, IAM roles                                       |
| **EKS**            | Managed Kubernetes service                           | Deploy and manage Kubernetes clusters                    | Simplifies Kubernetes management, integrated with AWS services                                                         |

