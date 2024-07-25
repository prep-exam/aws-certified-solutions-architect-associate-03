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






*This content is created using ChatGPT.*

