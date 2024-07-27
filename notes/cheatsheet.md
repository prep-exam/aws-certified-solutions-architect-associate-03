# AWS Cheat Sheet

## **Security**
- **Amazon CloudWatch**: ![#FFA07A](https://via.placeholder.com/15/FFA07A/000000?text=+) Metrics, Logs, Alarms
- **AWS CloudTrail**: ![#FFA07A](https://via.placeholder.com/15/FFA07A/000000?text=+) Audit Events
- **AWS WAF**: ![#FF6347](https://via.placeholder.com/15/FF6347/000000?text=+) Firewall, SQL Injection, Cross-Site Scripting (XSS), Layer 7 Attacks
- **AWS Shield**: ![#FF6347](https://via.placeholder.com/15/FF6347/000000?text=+) DDoS Attack, Layer 3 & 4 Attacks
- **Amazon Macie**: ![#FFD700](https://via.placeholder.com/15/FFD700/000000?text=+) Sensitive Data, Personally Identifiable Information (PII)
- **Amazon Inspector**: ![#FFD700](https://via.placeholder.com/15/FFD700/000000?text=+) EC2 Security Assessment, Unintended Network Accessibility
- **Amazon GuardDuty**: ![#98FB98](https://via.placeholder.com/15/98FB98/000000?text=+) Analyze VPC Flow Logs, Threat Detection
- **AWS VPN**: ![#98FB98](https://via.placeholder.com/15/98FB98/000000?text=+) Online Network Connection, Long-term Continuous Transfer, Low to Moderate Bandwidth
- **AWS Direct Connect**: ![#98FB98](https://via.placeholder.com/15/98FB98/000000?text=+) Private Secure Dedicated Connection, Long-term Continuous Transfer, High Bandwidth

## **Application Integration**
- **Amazon SNS**: ![#00BFFF](https://via.placeholder.com/15/00BFFF/000000?text=+) Serverless, Pub/Sub, Fan-Out
- **Amazon SQS**: ![#00BFFF](https://via.placeholder.com/15/00BFFF/000000?text=+) Serverless, Decoupled, Queue, Fan-Out
- **Amazon MQ**: ![#1E90FF](https://via.placeholder.com/15/1E90FF/000000?text=+) ActiveMQ
- **Amazon SWF**: ![#1E90FF](https://via.placeholder.com/15/1E90FF/000000?text=+) Serverless, Simple Workflow Service, Decoupled, Task Coordinator, Distributed & Background Jobs
- **AWS Step Functions (SF)**: ![#00FF00](https://via.placeholder.com/15/00FF00/000000?text=+) Orchestrate/Coordinate Lambda Functions and ECS Containers into a Workflow
- **AWS OpsWorks**: ![#00FF00](https://via.placeholder.com/15/00FF00/000000?text=+) Chef & Puppet

## **Storage**
- **EBS**: ![#FF69B4](https://via.placeholder.com/15/FF69B4/000000?text=+) Block Storage Volume for EC2
- **EFS**: ![#FF69B4](https://via.placeholder.com/15/FF69B4/000000?text=+) Network File System for EC2, Concurrent Access
- **Amazon S3**: ![#FF4500](https://via.placeholder.com/15/FF4500/000000?text=+) Serverless, Block Storage - Photos & Videos, Website Hosting
- **Amazon Athena**: ![#FF4500](https://via.placeholder.com/15/FF4500/000000?text=+) Query Data in S3 Using SQL
- **AWS Snow Family**: ![#32CD32](https://via.placeholder.com/15/32CD32/000000?text=+) Offline Data Migration, Petabyte to Exabyte Scale
- **AWS DataSync**: ![#32CD32](https://via.placeholder.com/15/32CD32/000000?text=+) Online Data Transfer, Immediate One-Time Transfer
- **AWS Storage Gateway**: ![#32CD32](https://via.placeholder.com/15/32CD32/000000?text=+) Hybrid Storage Between On-Premises and AWS

## **Compute**
- **AWS Lambda**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Serverless, FaaS

## **Database**
- **Amazon RDS**: ![#FFB6C1](https://via.placeholder.com/15/FFB6C1/000000?text=+) Relational Database - PostgreSQL, MySQL, MariaDB, Oracle, SQL Server
- **Amazon Aurora**: ![#FFB6C1](https://via.placeholder.com/15/FFB6C1/000000?text=+) Relational Database - Amazon-Owned
- **Amazon DynamoDB**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Serverless, Key-Value NoSQL Database - Amazon-Owned
- **Amazon DocumentDB**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Document Database, JSON Documents - MongoDB
- **Amazon Neptune**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Graph Database, Social Media Relationship
- **Amazon Timestream**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Time Series Database
- **Amazon Redshift**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Columnar Database, Analytics, BI, Parallel Query
- **Amazon ElastiCache**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Redis and Memcached, In-Memory Cache
- **Amazon EMR**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Elastic MapReduce, Big Data - Apache Hadoop, Spark, Hive, HBase, Flink, Hudi
- **Amazon Elasticsearch Service**: ![#D8BFD8](https://via.placeholder.com/15/D8BFD8/000000?text=+) Elasticsearch, ELK

## **Microservices**
- **Elastic Container Registry (ECR)**: ![#FF4500](https://via.placeholder.com/15/FF4500/000000?text=+) Docker Image Repository, DockerHub
- **Elastic Container Service (ECS)**: ![#FF4500](https://via.placeholder.com/15/FF4500/000000?text=+) Docker Container Management System
- **AWS Fargate**: ![#FF4500](https://via.placeholder.com/15/FF4500/000000?text=+) Serverless ECS
- **AWS X-Ray**: ![#FF4500](https://via.placeholder.com/15/FF4500/000000?text=+) Trace Request, Debug

## **Developer Tools**
- **AWS CodeCommit**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Git-Based Source Code Repository
- **AWS CodeBuild**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) CI, Code Compile, Build & Test
- **AWS CodeDeploy**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Code Deployment to EC2, Fargate, and Lambda
- **AWS CodePipeline**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) CI/CD Pipelines, Rapid Software or Build Release
- **AWS CloudShell**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) CLI, Browser-Based Shell
- **AWS Elastic Beanstalk**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) PaaS, Quick Deploy Applications - Java-Tomcat, PHP/Python-Apache HTTP Server, Node.js-Nginx
- **Amazon Workspaces**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Desktop-as-a-Service, Virtual Windows or Linux Desktops
- **Amazon AppStream 2.0**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Install Applications on Virtual Desktop and Access it from Mobile, Tablet, or Remote Desktop through Browser
- **AWS CloudFormation**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Infrastructure as Code, Replicate Infrastructure
- **AWS Certificate Manager (ACM)**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Create, Renew, Deploy SSL/TLS Certificates to CloudFront and ELB
- **AWS Migration Hub**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Centralized Tracking on the Progress of All Migrations Across AWS
- **AWS Glue**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Data ETL (Extract, Transform, Load), Crawler, Data Catalog
- **AWS AppSync**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) GraphQL
- **Amazon Elastic Transcoder**: ![#D3D3D3](https://via.placeholder.com/15/D3D3D3/000000?text=+) Media (Audio, Video) Converter
