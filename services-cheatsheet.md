# EC2 Instances

## Instance Types
- **Over 300 EC2 instance types across 5 families:**
  - General Purpose
  - Memory-Optimized
  - Storage-Optimized
  - Compute-Optimized
  - Accelerated Computing
- **Compute-Optimized Examples:**
  - C4 instances (Haswell chips)
  - C5 instances (Skylake with Nitro system)
![image](https://github.com/user-attachments/assets/6ce4ffbc-edb1-4034-a407-03313edc52a5)

## Instance Purchasing Options
- **On-Demand Instances**: Default option for short-term, ad-hoc jobs that can’t be interrupted.
- **On-Demand Capacity Reservations**: Reserve capacity for specific time blocks, e.g., 9am-5pm daily.
- **Spot Instances**: Highest discount (50-90%), but can be terminated with 2-minute notice. Good for grid and high-performance computing.
- **Reserved Instances**: For long-term workloads with 1 or 3-year commitments, offering 40-60% discounts.
- **Dedicated Instances**: Run on hardware dedicated to one customer.
- **Dedicated Hosts**: Fully dedicated, physically isolated servers. Useful for specific software licenses (e.g., IBM, Oracle) and compliance needs.
- **Bare Metal Instances**: Access to hardware feature sets (e.g., Intel hardware).
![image](https://github.com/user-attachments/assets/4261a052-a947-4a7e-856f-fd45b44b2dde)


## Launching Instances
- **Launch Templates**: Create instances with stored parameters (instance type, AMI, key pair, security groups). Use with auto-scaling groups.
  - **User Data**: Pass up to 16KB of data at launch for startup scripts.
  - **Instance Metadata**: Access via direct URI or Instance Metadata Query Tool.
- **Public/Private DNS**: Default VPC instances have public and private DNS/IP. Non-default VPC instances might not have public DNS depending on configuration.
- **Common Launch Errors**:
  - InsufficientInstanceCapacity
  - InstanceLimitExceeded
- **Instance Termination Causes**: EBS issues (volume limit, corrupt snapshot), missing parts in the AMI.
- **Root Device Volumes**: Each instance has an EBS or Instance Store volume. Use block device mapping for additional volumes.
- **Run Command**: Manage instances via AWS Management Console, CLI, or SDK for tasks like software installation and script execution.

![image](https://github.com/user-attachments/assets/6a8ed010-eda2-4b8c-80d2-b91bcfc3d37b)



## Placement Groups
- **Cluster Placement Group**: Packs instances close together within an AZ for low latency, high throughput. Ideal for HPC.
- **Partition Placement Group**: Separates instances into partitions with no shared hardware. Suitable for large distributed workloads like Hadoop.
- **Spread Placement Group**: Distributes instances across distinct hardware to minimize correlated failures.

![image](https://github.com/user-attachments/assets/56869dcf-d4ad-4c06-bf56-10bbb35ecca5)


## Scaling Instances
- **Auto-Scaling Groups (ASG)**: Automatically manage instance launching and stopping.
  - **Elastic Load Balancer (ELB)**: Distributes traffic among instances.
  - **ASG Policies**:
    - **Simple**: Manually maintain instance numbers.
    - **Scheduled**: Scale based on schedule (e.g., daily traffic spikes).
    - **Dynamic**: Scale in response to events or alarms.
    - **Step**: Configure scaling changes based on multiple events.
    - **Target Tracking**: Uses custom metrics for scaling.
  - **Cooldown Period**: Reducing cooldown periods can save costs by terminating unneeded instances faster.
- **Enhanced Networking**: Provides higher bandwidth, higher PPS, and lower inter-instance latency.

![image](https://github.com/user-attachments/assets/0b6fbd42-519d-41af-8e8d-d6b7cbabad24)


Certainly! Here's the content formatted for an IT blog page, making it easy to read and understand.

 

# AWS VPC, Subnets, and Networking

## Virtual Private Cloud (VPC)
A VPC is a virtual network that closely resembles a traditional network you'd operate in your own data center.

### Key Components
- **Subnets**: After creating a VPC, you can add subnets, which are ranges of IP addresses in your VPC.
- **Route Tables**: Determine where network traffic from your subnet or gateway is directed.
- **Gateway**: Connects your VPC to another network (e.g., internet gateway connects your VPC to the internet).
- **VPC Endpoint**: Connects to AWS services privately, without an internet gateway or NAT device.
- **VPC Peering**: Routes traffic between resources in two VPCs.
- **Transit Gateway**: Acts as a central hub, routing traffic between your VPCs, VPN connections, and AWS Direct Connect connections.
- **AWS VPN**: Connects your VPCs to your on-premises networks.

## Subnets
A VPC is housed within a Region, and a subnet maps 1-to-1 with an AZ (Availability Zone). For high availability, you need at least 2 subnets in your VPC to span 2 AZs.

### Subnet Characteristics
- **Main Route Table**: When you create a new subnet, it's automatically associated with the main route table.

### Example VPC/Subnet Configurations
- **Single Public Subnet**: For single-tier, public-facing web apps (e.g., blog or simple website).
- **Public and Private Subnets**: For multi-tier web apps where web servers are in the public subnet and databases in the private subnet.

## Public Subnet vs. Private Subnet

### Public Subnets
- **Route Table**: Routes to an Internet Gateway.
- **EC2 Instances**: Auto-assigned a public IP address or ENI.
- **Security**: Security groups and network ACLs must allow SSH traffic (port 22) for admin configuration.

### Private Subnets
- **Outbound Traffic**: Routed to a NAT device installed in the Public Subnet and connected to an Internet Gateway.
- **NAT Device**: 
  - **NAT Gateway**: Managed by AWS and highly available.
  - **NAT Instance**: Manual work but can be used as a bastion host/jump box.
- **EC2 Instances**: Do not have public IP or ENI.
- **Access**: Use a bastion host ("jump box") for SSH access (port 22).

## VPC Endpoints

### Interface Endpoints
- Privately connect your VPC to AWS services, services hosted by other AWS accounts, and supported AWS Marketplace services as if they were in your VPC.
- Powered by AWS PrivateLink, does not go over the internet.
- No need for an internet gateway, NAT device, DX connection, or VPN.
- Is an ENI with a private IP address in the specified subnet, directing traffic to the specified service.
- Uses DNS to direct traffic to the service, protected by a Security Group.

### Gateway Endpoints
- Direct traffic to S3 or DynamoDB using private IP addresses.
- Does not enable AWS PrivateLink.
- Route traffic from your VPC to the gateway endpoint using route tables.
- Protected by VPC endpoint policies rather than Security Groups.

## Types of Network Adapters
- **ENI (Elastic Network Interface)**: Basic type.
- **ENA (Elastic Network Adapter)**: For enhanced networking, high bandwidth, and low latency.
- **EFA (Elastic Fabric Adapter)**: For high-performance computing.

## Security Groups vs. Network ACLs (NACL)

### Security Groups
- **Level**: Instance level.
- **Rules**: No deny rules, stateful.
- **Evaluation**: Evaluate all rules together.
- **Traffic**: Cannot block traffic by country.
- **Inbound/Outbound Rules**:
  - Default state: Outbound allows all traffic, inbound denied by default.

### Network ACLs
- **Level**: Subnet level, applies to all instances within the subnet.
- **Rules**: Accept and deny, stateless.
- **Evaluation**: Processes rules in order.
- **Traffic**: Cannot block traffic by country.
- **Inbound/Outbound Rules**:
  - Default state: All inbound/outbound traffic allowed by default.
  - Custom NACL: Denies all inbound/outbound traffic by default.

 ![image](https://github.com/user-attachments/assets/7f894dac-5ef2-4f13-8263-25fffb6bdc20)


Here's a more readable and organized format for the content about Amazon Route 53, Elastic Load Balancers, AWS Direct Connect, AWS Transit Gateway, VPN Connections, and AWS CloudFormation:

---

# AWS Route 53

## Routing Policies
- **Geolocation Routing**: Routes traffic based on the location of the user.
- **Geoproximity Routing**: Routes traffic based on proximity to resources.
- **Weighted Routing**: Splits traffic based on specified percentages.
- **Health Check**: Checks the health of resources and routes traffic only to healthy resources.
- **Failover Policy**: 
  - **Active/Passive**: Uses a backup resource if the primary fails. Manual intervention may be needed for failback.
  - **Active/Active**: Returns multiple resources. Requires policies like latency or weighted, but not failover.
  - **Combination**: Uses multiple policies combined in a tree for complex DNS failover.

## Routing Records
- **Alias Records**:
  - Route traffic to AWS resources like ELBs, APIs, CloudFront, S3, Elastic Beanstalk, VPC endpoints.
  - Can point from one record to another within the same hosted zone.
  - Route 53 responds with IP addresses.
- **CNAME Records**:
  - Redirect DNS queries to other DNS records.
  - Cannot be used for apex domain names.
- **PTR Records**:
  - Perform reverse lookups by mapping an IP address to a DNS name.

![image](https://github.com/user-attachments/assets/df8574a4-6be6-486d-a247-ddd4dea7bbb9)


---

# AWS Elastic Load Balancers (ELBs)

## Types of Load Balancers
- **Application Load Balancer (ALB)**:
  - Operates at Layer 7 (HTTP/HTTPS).
  - Supports path-based and host-based routing.
  - Can route requests to multiple ports on ECS container instances.
  - Supports authentication with OIDC-compliant IDPs (e.g., Google, Facebook) via Cognito.
  - Performs health checks and logs access information to S3.

- **Network Load Balancer (NLB)**:
  - Operates at Layer 4 (TCP/SSL).
  - Handles millions of requests per second with low latency.
  - Does not support path-based or host-based routing.

- **Classic Load Balancer (CLB)**:
  - Operates using TCP, SSL, HTTP, and HTTPS.
  - Less efficient at high throughput and low latency compared to NLB.
  - Does not support load balancing to multiple ports on an instance.

![image](https://github.com/user-attachments/assets/786a568a-df99-4ff0-be7a-4b60f8549a87)



---

# AWS Direct Connect (DX)

## Overview
- Connects on-prem data centers to one or multiple VPCs.
- Can take over a month to set up.
- For resilience, consider adding a second DX connection or an IPSec VPN connection for short-term redundancy.

## Virtual Interfaces
- **Private Virtual Interface (VIF)**: Accesses a VPC using private IP addresses.
- **Public Virtual Interface (VIF)**: Accesses AWS public services using public IP addresses.
- **Transit Virtual Interface (VIF)**: Accesses VPC Transit Gateways within a Region.
- **Hosted Virtual Interface (VIF)**: Allows another AWS account to access your DX.

## Data Transfer
- Use AWS DataSync for large data transfers to S3, EFS, FSx, NFS, SMB shares, or AWS Snowcone.
- Use DMS for copying databases.

![image](https://github.com/user-attachments/assets/01a0dc6f-4dc2-402b-81ac-28355bc5d444)

---

# AWS Transit Gateway

## Overview
- Acts as a central hub for connecting on-prem networks and VPCs.
- Simplifies operations by reducing the complexity of routing tables.
- Provides additional features compared to VPC peering.

## Connection Pattern
- **On-prem -> DX -> DX Location -> Transit Virtual Interface -> Transit Gateway Association -> Transit Gateway -> Multiple VPCs**

---

# VPN Connections

## Overview
- VPN connections go over the internet.
- **AWS Managed Site-to-Site VPN**: Connects a Customer Gateway on the customer side to a Virtual Private Gateway (VPG) at the edge of your VPC.

---

# AWS CloudFormation

## Overview
- **Provision Infrastructure**: Use text-based templates to describe resources and their settings.
- **Template Management**: Manages template history similar to source control.
- **Update Methods**:
  - **Direct Update**: Immediately deploys changes.
  - **Change Sets**: Previews changes before deployment.
- **AWS SAM (Serverless Application Model)**: Extension of CloudFormation for serverless application management.

![image](https://github.com/user-attachments/assets/58c01651-11fc-49f2-ac97-9e7e391e6c24)

---

This format should help in understanding and retaining key concepts more effectively.

*This content is created using ChatGPT.*

