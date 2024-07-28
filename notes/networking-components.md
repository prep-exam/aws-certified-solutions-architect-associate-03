


### <span style="color:blue">Amazon VPC Overview</span>

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

### <span style="color:green">VPC (Virtual Private Cloud)</span>
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

### <span style="color:darkorange">VPC Peering </span>
VPC peering connects two VPCs over a direct network route using private IP addresses.

#### Key Features
- **Behavior**: Instances in peered VPCs act as if they are on the same network.
- **CIDR**: No overlapping CIDR blocks allowed.
- **Non-Transitive**: VPC peering is not transitive (A-B and B-C does not imply A-C).
- **Route Tables**: Update route tables in both VPCs for communication.
- **Regions and Accounts**: Can peer VPCs in the same or different regions and AWS accounts.

### <span style="color:green">Subnets </span>
A subnet is a range of IP addresses in your VPC.

#### Key Features
- **Association**: Each subnet is tied to one Availability Zone (AZ), one Route Table, and one Network ACL.
- **CIDR Block**: Assign one CIDR block per subnet within the VPC's CIDR range, ensuring no overlap with other subnets.
- **Reserved IPs**: AWS reserves the first 4 and the last IP in each subnet.
- **Public Subnets**: Enable auto-assign public IPv4 addresses for EC2 instances.
- **Multi-Tier Architecture**: For regions with 3 AZs, create 3 private and 3 public subnets for a highly available architecture. Public subnets host API gateways and ALBs, while private subnets host EC2 instances, Lambdas, and databases.

 

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


### DNS Record Types

#### <span style="color:blue">CNAME Record</span>

- **Definition**: Canonical Name Record
- **Purpose**: Points a hostname to another hostname.
- **Usage**:
  - Only works with subdomains (e.g., `something.mydomain.com`).
  - Cannot be used for root domains.
- **Example**: 
  - `www.example.com` CNAME to `example.com`.

#### <span style="color:green">A Record</span>

- **Definition**: Address Record
- **Purpose**: Maps a hostname to an IPv4 address.
- **Usage**:
  - Works with both root domains and subdomains (e.g., `mydomain.com` or `sub.mydomain.com`).
  - Points to AWS resources such as ALB, API Gateway, CloudFront, S3 Bucket, Global Accelerator, Elastic Beanstalk, VPC interface endpoint, etc.
- **Example**: 
  - `api.example.com` A record pointing to `192.0.2.1`.

#### <span style="color:orange">AAAA Record</span>

- **Definition**: IPv6 Address Record
- **Purpose**: Maps a hostname to an IPv6 address.
- **Usage**:
  - Works with both root domains and subdomains.
  - Used for AWS resources with IPv6 addresses.
- **Example**: 
  - `ipv6.example.com` AAAA record pointing to `2001:db8::1`.

## <span style="color:purple">Summary Table</span>

| **Record Type** | **Purpose**                                       | **Usage**                                       | **Example**                    |
|-----------------|---------------------------------------------------|-------------------------------------------------|--------------------------------|
| **CNAME**       | Points hostname to another hostname              | Subdomains only                                | `www.example.com` CNAME to `example.com` |
| **A**           | Maps hostname to an IPv4 address                 | Root domains and subdomains                    | `api.example.com` A record to `192.0.2.1` |
| **AAAA**        | Maps hostname to an IPv6 address                 | Root domains and subdomains                    | `ipv6.example.com` AAAA to `2001:db8::1` |

### DNS Routing Policies in Amazon Route 53

#### <span style="color:blue">Simple Routing Policy</span>

- **Definition**: Routes traffic to a single resource or multiple resources.
- **Purpose**: To route traffic to specific IPs using a single DNS record. Allows returning multiple IPs after resolving DNS.
- **Usage**:
  - Use when you have a single resource or multiple resources that should be accessible equally.
- **Example**: 
  - A record for `example.com` might resolve to multiple IPs: `192.0.2.1`, `198.51.100.1`.

#### <span style="color:green">Weighted Routing Policy</span>

- **Definition**: Routes traffic based on assigned weights.
- **Purpose**: To distribute traffic among multiple resources based on specified weights (0 to 255).
- **Usage**:
  - Create multiple DNS records with different weights to control the proportion of traffic each resource receives.
- **Example**:
  - DNS records: `A` record with weight 70, another `A` record with weight 20, and another `A` record with weight 10.

#### <span style="color:orange">Latency Routing Policy</span>

- **Definition**: Routes traffic based on the lowest latency between the client and AWS regions.
- **Purpose**: To direct users to the AWS region that provides the lowest latency for them.
- **Usage**:
  - Create DNS records for multiple AWS regions to improve user experience by reducing latency.
- **Example**:
  - DNS records with regions: `us-east-1`, `eu-west-2`, `ap-east-1`.

#### <span style="color:red">Failover Routing Policy</span>

- **Definition**: Routes traffic to a primary resource and automatically fails over to a secondary resource if the primary is unhealthy.
- **Purpose**: To ensure high availability by routing traffic from a primary to a secondary resource in case of failure.
- **Usage**:
  - Create DNS records for both primary and secondary IPs. 
  - Mandatory to create health checks for both IPs and associate them with the DNS records.
- **Example**:
  - Primary IP `192.0.2.1`, Secondary IP `198.51.100.1`.

#### <span style="color:purple">Geolocation Routing Policy</span>

- **Definition**: Routes traffic based on the geographic location of the user.
- **Purpose**: To direct users to resources based on their continent or country.
- **Usage**:
  - Create DNS records for specific locations and a default record for unmatched locations.
- **Example**:
  - Create records for `US`, `Europe`, `Asia`, and a default location policy.

#### <span style="color:teal">Geoproximity Routing Policy</span>

- **Definition**: Routes traffic based on the geographic location of the user with a bias value.
- **Purpose**: To control traffic distribution based on user location with a bias value for more or less traffic.
- **Usage**:
  - Set a bias value to increase (1 to 99) or decrease (-1 to -99) traffic from specific locations.
- **Example**:
  - A bias value of 20 increases traffic from a specific region.

#### <span style="color:magenta">Multivalue Answer Routing Policy</span>

- **Definition**: Returns up to 8 healthy IP addresses after resolving DNS.
- **Purpose**: Acts as a client-side load balancer and allows for multiple healthy IPs.
- **Usage**:
  - Create multiple DNS records with associated health checks. Provides high availability but expect some downtime during TTL if an EC2 instance becomes unhealthy.
- **Example**:
  - Create 3 DNS records with health checks to return up to 8 healthy IPs.

#### <span style="color:gray">Summary Table</span>

| **Routing Policy**   | **Purpose**                                         | **Usage**                                           | **Example**                    |
|----------------------|-----------------------------------------------------|-----------------------------------------------------|--------------------------------|
| **Simple**           | Route traffic to specific IPs                     | Single or multiple IPs                            | Multiple IPs for `example.com` |
| **Weighted**         | Distribute traffic based on weights                | Control traffic proportion                        | Weights 70, 20, 10            |
| **Latency**          | Route traffic based on lowest latency              | Direct users to nearest AWS region                 | Regions: `us-east-1`, `eu-west-2` |
| **Failover**         | Route traffic from primary to secondary on failure | Ensure high availability                           | Primary and secondary IPs      |
| **Geolocation**      | Route traffic based on user location               | Specific regions or countries                      | Records for `US`, `Europe`     |
| **Geoproximity**     | Route traffic based on location with bias value    | Control traffic with positive/negative bias        | Bias value for specific region |
| **Multivalue Answer**| Return up to 8 healthy IPs                         | Acts as client-side load balancer                  | Up to 8 IPs with health checks |


#### DNS Failover in Amazon Route 53

###### <span style="color:blue">Active-Active Failover</span>

- **Definition**: All resources are active and can handle traffic simultaneously.
- **Purpose**: To ensure that all resources are available the majority of the time, distributing traffic across multiple active resources.
- **Configuration**:
  - All DNS records have the same name, type, and routing policy (e.g., weighted or latency).
  - Traffic is distributed based on the routing policy, with all resources actively handling requests.
- **Usage**:
  - Ideal for scenarios where you want to balance the load across multiple resources and ensure high availability.
- **Example**:
  - Multiple `A` records with weights (e.g., 50, 30, 20) to distribute traffic among several servers.
  - `example.com` resolves to multiple IP addresses with a weighted routing policy.

###### <span style="color:green">Active-Passive Failover</span>

- **Definition**: Primary resources handle traffic under normal conditions, and secondary resources are used only when primary resources fail.
- **Purpose**: To ensure high availability by having a standby resource that takes over if the primary resource fails.
- **Configuration**:
  - Create two records: one for the primary resource and one for the secondary resource.
  - Use the failover routing policy to route traffic from the primary to the secondary resource in case of failure.
  - Health checks must be configured for both the primary and secondary records.
- **Usage**:
  - Suitable for scenarios where you need a primary resource for handling traffic and a standby resource for failover.
- **Example**:
  - Primary `A` record for `example.com` with IP `192.0.2.1` and a secondary `A` record with IP `198.51.100.1`.
  - Health checks monitor the primary resource, and traffic fails over to the secondary IP if the primary fails.

###### <span style="color:purple">Summary Table</span>

| **Failover Type**   | **Definition**                                     | **Purpose**                                            | **Configuration**                           | **Example**                         |
|---------------------|-----------------------------------------------------|--------------------------------------------------------|---------------------------------------------|-------------------------------------|
| **Active-Active**   | All resources are active and handle traffic        | Ensure all resources are available most of the time   | Same name, type, and routing policy for all | Weighted records distributing traffic |
| **Active-Passive**  | Primary handles traffic, secondary takes over on failure | High availability with standby resource              | Two records: primary and secondary with failover policy | Primary `192.0.2.1`, Secondary `198.51.100.1` |

### AWS Global Accelerator

##### <span style="color:blue">Overview</span>

- **Definition**: A global service designed to improve the performance of your applications by lowering latency, reducing jitter, and increasing throughput compared to the public internet.
- **Purpose**: Enhances global application performance using AWS's global network and edge locations to find the most optimal pathway for traffic.

##### <span style="color:green">How It Works</span>

1. **Create Global Accelerator**:
   - Provision two anycast static IP addresses that act as a fixed entry point for your applications.
   - These IP addresses are used to route traffic from clients to the nearest AWS edge location.

2. **Register Endpoints**:
   - Register one or more endpoints with Global Accelerator. Each endpoint can include:
     - Network Load Balancer (NLB)
     - Application Load Balancer (ALB)
     - EC2 Instances
     - S3 Buckets
     - Elastic IPs
   - You can configure multiple AWS resources as endpoints for improved redundancy and availability.

3. **Set Weights**:
   - Assign weights to each endpoint to control the proportion of traffic routed to each one. This allows for traffic distribution based on the assigned weights.

4. **Health Monitoring**:
   - Global Accelerator performs health checks on all registered AWS resources.
   - Traffic is routed only to healthy resources based on the health checks.

##### <span style="color:orange">Benefits</span>

- **Improved Performance**:
  - Lower latency and jitter due to optimized routing over AWS’s global network.
- **Increased Throughput**:
  - Enhanced application performance compared to traditional public internet routes.
- **Global Reach**:
  - Utilizes AWS edge locations worldwide to provide a better experience for global users.
- **Resilience**:
  - Automatically routes traffic away from unhealthy resources, ensuring high availability.

##### <span style="color:purple">Summary Table</span>

| **Feature**            | **Description**                                      |
|------------------------|------------------------------------------------------|
| **Global Service**     | Improves global application performance.            |
| **Anycast IPs**        | Provision two static anycast IP addresses.           |
| **Endpoints**          | Register NLB, ALB, EC2, S3, or Elastic IPs.          |
| **Weighting**          | Assign weights to control traffic distribution.      |
| **Health Checks**      | Monitors and routes traffic based on resource health.|




### <span style="color:blue">Subnets Cheat Sheet</span>

#### <span style="color:blue">Key Points</span>
- Each subnet maps to a single Availability Zone.
- Automatically associated with the main route table for the VPC upon creation.
- Public subnet: Traffic routed to an Internet gateway.
- Allowed block size in VPC: /16 netmask (65,536 IP addresses) to /28 netmask (16 IP addresses).

#### <span style="color:blue">Subnets Overview</span>
- **CIDR Block for VPC**: Specify a range of IPv4 addresses (e.g., 10.0.0.0/16).
- **Subnets in Availability Zones**: Add one or more subnets per zone.
- **CIDR Block for Subnet**: A subset of the VPC CIDR block, must not overlap with existing blocks.
- **Types of Subnets**:
  - **Public Subnet**: Has an Internet gateway.
  - **Private Subnet**: No Internet gateway.
  - **VPN-only Subnet**: Has a virtual private gateway.

#### <span style="color:blue">IPv4 CIDR Block</span>
- Block size: /16 netmask (65,536 IP addresses) to /28 netmask (16 IP addresses).
- First four and last IP addresses in a subnet CIDR block are reserved.
- Cannot resize existing CIDR blocks.
- Route added to VPC route tables automatically when a CIDR block is associated.

#### <span style="color:blue">Subnet Routing</span>
- Each subnet must be associated with a route table.
- Automatically associated with the main route table for the VPC upon creation.
- Change the association or the contents of the main route table.
- **NAT Gateway/NAT Instance**: Allows outbound connections to the internet over IPv4 while preventing unsolicited inbound connections.
- **Egress-only Internet Gateway**: Allows outbound-only communication over IPv6.

#### <span style="color:blue">Subnet Security</span>
- **Security Groups**: Control inbound and outbound traffic for instances.
  - Up to five security groups can be associated with an instance.
  - Default group if none specified; no inbound rules by default.
  - Outbound rule allowing all traffic by default.
- **Network Access Control Lists (ACLs)**: Control inbound and outbound traffic for subnets.
  - Associated with each subnet, default if none specified.
  - Can be associated with multiple subnets but only one ACL per subnet.
  - Rules are evaluated in order, starting with the lowest numbered rule.
  - Default ACL allows all traffic; custom ACLs need rules for ephemeral ports (32768-65535) and port range (1024-65535) for NAT Gateway, ELB, or Lambda functions.
- **Flow Logs**: Capture IP traffic information for network interfaces, published to CloudWatch Logs.
  - Diagnose security group rules, monitor traffic, determine traffic direction.
  - Collected outside of network traffic path; no impact on performance.
  - Several minutes delay to start collecting data; sent to Amazon S3 for analysis.
  - Do not capture real-time log streams or IP traffic to/from link-local or AWS-reserved IPv4 addresses.

### <span style="color:blue">Security Groups vs. Network ACLs</span>

| **Aspect**           | **Security Group**                     | **Network ACL**                         |
|----------------------|----------------------------------------|-----------------------------------------|
| **Level**            | Instance level                         | Subnet level                            |
| **Rules Supported**  | ALLOW rules only                       | ALLOW and DENY rules                    |
| **State**            | Stateful: Return traffic allowed       | Stateless: Return traffic must be allowed explicitly |
| **Rule Evaluation**  | Evaluate all rules before allowing traffic | Process rules in number order           |
| **Application**      | Applies to EC2 instances and similar services using EC2 as a backend | Automatically applies to all instances in the subnets it’s associated with |
| **Specification**    | Specified when launching instances or associated later | Automatically associated with instances in subnets |

#### <span style="color:blue">Diagram of Security Groups and NACLs in a VPC</span>
*(Here you would include a visual diagram showing the relationship and application of security groups and network ACLs within a VPC.)*

 