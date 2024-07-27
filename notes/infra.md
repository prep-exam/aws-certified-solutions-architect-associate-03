### <span style="color:blue">AWS Infrastructure</span>

#### <span style="color:green">AWS Region</span>

AWS regions are physical locations around the world having a cluster of data centers.

| **AWS Region**               | **Code**        |
|------------------------------|-----------------|
| US East (N. Virginia)        | us-east-1       |
| US East (Ohio)               | us-east-2       |
| US West (N. California)      | us-west-1       |
| US West (Oregon)             | us-west-2       |
| Africa (Cape Town)           | af-south-1      |
| Asia Pacific (Hong Kong)     | ap-east-1       |
| Asia Pacific (Mumbai)        | ap-south-1      |
| Asia Pacific (Osaka)         | ap-northeast-3  |
| Asia Pacific (Seoul)         | ap-northeast-2  |
| Asia Pacific (Singapore)     | ap-southeast-1  |
| Asia Pacific (Sydney)        | ap-southeast-2  |
| Asia Pacific (Tokyo)         | ap-northeast-1  |
| Canada (Central)             | ca-central-1    |
| Europe (Frankfurt)           | eu-central-1    |
| Europe (Ireland)             | eu-west-1       |
| Europe (London)              | eu-west-2       |
| Europe (Milan)               | eu-south-1      |
| Europe (Paris)               | eu-west-3       |
| Europe (Stockholm)           | eu-north-1      |
| Middle East (Bahrain)        | me-south-1      |
| South America (São Paulo)    | sa-east-1       |

- **Note:** You need to select the region for most AWS services such as EC2, ELB, S3, Lambda, etc.
- **Global AWS Services:** IAM, AWS Organizations, Route 53, CloudFront, WAF, etc. are not region-specific.
- **Availability Zones (AZs):** Each AWS Region consists of multiple AZs (usually 3, with a minimum of 2 and a maximum of 6).

#### <span style="color:green">AZ (Availability Zones)</span>

An AZ is a discrete data center with redundant power, networking, and connectivity.

- All AZs in a region are interconnected with high-bandwidth, low-latency networking.
- Deploy applications across multiple AZs for high availability, scalability, and fault tolerance.
- Example: For high availability in `us-east-2`, you could place 3 instances in each of 3 AZs or 6 instances in each of 2 AZs.

---

### <span style="color:blue">Security, Identity & Compliance</span>

#### <span style="color:green">IAM (Identity and Access Management)</span>

IAM is used to manage access to users and resources. It is a global service and is free.

- **Root Account:** Created by default with full administrator access. Should not be used for daily operations.
- **Users:** Mapped to physical users. Each user logs into AWS with their own account and password.
- **Groups:** Can contain multiple users but not other groups.
- **Policies:** JSON documents that define access permissions for users, groups, and roles.

**Policy Structure:**
```json
{
    "Version":"2012-10-17",
    "Statement":[
        {
            "Sid": "Deny-Barclay-S3-Access",
            "Effect":"Deny",
            "Principal": { "AWS": ["arn:aws:iam:123456789012:barclay"] },
            "Action": [ "s3:GetObject", "s3:PutObject", "s3:List*" ],
            "Resource": ["arn:aws:s3:::mybucket/*"]
        },
        {
            "Effect": "Allow",
            "Action": "iam:CreateServiceLinkedRole",
            "Resource": "*",
            "Condition": {
                "StringLike": {
                    "iam:AWSServiceName": [
                        "rds.amazonaws.com",
                        "rds.application-autoscaling.amazonaws.com"
                    ]
                }
            }
        }
    ]
}
```


Certainly! Here’s the information formatted in Markdown:

---

### <span style="color:green">Access AWS Programmatically</span>

#### AWS Management Console
- **Authentication:** Use password + MFA (Multi-Factor Authentication).

#### AWS CLI or SDK
- **Credentials:** Use Access Key ID (~username) and Secret Access Key (~password).
- **Version Check:**
  ```bash
  $ aws --version
  ```
- **Configuration:**
  ```bash
  $ aws configure
  AWS Access Key ID [None]:
  AWS Secret Access Key [None]:
  Default region name [None]:
  Default output format [None]:
  ```
- **Example Command:**
  ```bash
  $ aws iam list-users
  ```

#### AWS CloudShell
- **Description:** CLI tool accessible from the AWS Management Console browser interface.
- **Requirement:** Requires login to AWS.

---

### Access AWS for Non-IAM Users

Non-IAM users authenticate via Identity Federation and then access AWS resources using a temporary token provided by AWS STS (Security Token Service).

#### Identity Federation Methods

1. **SAML 2.0 (Old Method)**
   - **Integration:** Active Directory/ADFS.
   - **API:** `AssumeRoleWithSAML` STS API.

2. **Custom Identity Broker**
   - **Usage:** When the identity provider is not compatible with SAML 2.0.
   - **APIs:** `AssumeRole` or `GetFederationToken` STS API.

3. **Web Identity Federation**
   - **Usage:** Sign in using external identity providers (e.g., Amazon, Facebook, Google, OpenID Connect).
   - **Process:** Obtain the ID token from the identity provider, use AWS Cognito API to exchange it for a Cognito token, and then use `AssumeRoleWithWebIdentity` STS API.

4. **AWS Cognito**
   - **Recommendation:** Amazon's recommended identity provider.

5. **Amazon Single Sign-On (SSO)**
   - **Feature:** Provides a single sign-on token to access AWS without needing to call the STS API.

---

### AWS Directory Service

AWS Directory Service provides several options for managing Active Directory (AD) in AWS:

1. **AWS Managed Microsoft AD**
   - **Description:** Managed Microsoft Windows Server AD with a trust connection to on-premise Microsoft AD.
   - **Best For:** Full AD features, single sign-on for Windows workloads.

2. **AD Connector**
   - **Description:** Proxy service that redirects requests to on-premise Microsoft AD.
   - **Best For:** Using existing on-premise AD with compatible AWS services.

3. **Simple AD**
   - **Description:** Standalone AWS-managed AD compatible with Samba 4, providing basic directory features.
   - **Best For:** Basic directory needs, not connectable to on-premise AD.

4. **Amazon Cognito**
   - **Description:** User directory for sign-up and sign-in for mobile and web applications using Cognito User Pools.
   - **Note:** Unrelated to Microsoft AD.

---

Here's the information formatted in Markdown with color for better readability:

---

### <span style="color:green">Amazon Cognito</span>

#### <span style="color:blue">Cognito User Pools (CUP)</span>
- **Description:** User Pools is a user directory for sign-up and sign-in to mobile and web applications.
- **Usage:** Mainly used for authentication to access AWS services.
- **Features:**
  - Authenticates mobile app users through user pool directory or federated through third-party identity providers (IdPs) like Facebook, Google, Amazon, Apple, OIDC, and SAML IdPs.
  - After successful authentication, your web or mobile app receives user pool JWT tokens.
  - **JWT Token Uses:**
    - Retrieve temporary AWS credentials to access other AWS services.
    - Create a group in the user pool with an IAM role to access API Gateway, using JWT tokens to access Amazon API Gateway.

#### <span style="color:blue">Cognito Identity Pools (Federated Identity)</span>
- **Description:** Identity Pools are used for authorization to access AWS services.
- **Usage:** Authenticate users using User Pools and then exchange the token with Identity Pools, which use AWS STS to generate temporary AWS credentials.
- **Features:**
  - Provides temporary access to write to S3 buckets using social logins (e.g., Facebook, Google).
  - Supports guest users.

---

### <span style="color:green">AWS Key Management Service (KMS)</span>
- **Description:** AWS managed centralized key management service for creating, managing, and rotating customer master keys (CMKs) for encryption at rest.
- **Key Types:**
  - **Symmetric:** Single key for both encrypt and decrypt operations.
  - **Asymmetric:** Public/private key pair for encrypt/decrypt or sign/verify operations.
- **Features:**
  - Automatic master key rotation once per year.
  - Keeps older versions of master keys for decrypting old encrypted data.

---

### <span style="color:green">AWS CloudHSM</span>
- **Description:** AWS managed dedicated hardware security module (HSM) in AWS Cloud.
- **Usage:** Securely generate, store, and manage your own cryptographic keys.
- **Integration:** Uses industry-standard APIs like PKCS#11, Java Cryptography Extensions (JCE), and Microsoft CryptoNG (CNG) libraries.
- **Use Case:** Use KMS to create CMKs in a custom key store and store non-extractable key material in AWS CloudHSM for full control over encryption keys.

---

### <span style="color:green">AWS Systems Manager</span>

#### <span style="color:blue">Parameter Store</span>
- **Description:** Centralized secrets and configuration data management (e.g., passwords, database details).
- **Parameter Types:**
  - **String:** Plain text.
  - **StringList:** Comma-separated.
  - **SecureString:** KMS encrypted data.
- **Use Case:** Centralized configuration for dev/uat/prod environments, used by CLI, SDK, and Lambda functions.

#### <span style="color:blue">Run Command</span>
- **Description:** Automates common administrative tasks and performs one-time configuration changes on EC2 instances at scale.

#### <span style="color:blue">Session Manager</span>
- **Description:** Replaces the need for Bastions to access instances in private subnets.

---

### <span style="color:green">AWS Secrets Manager</span>
- **Description:** Stores, manages, and rotates secrets such as database credentials, API keys, and OAuth tokens.
- **Features:**
  - Native support for rotating RDS database credentials (MySQL, PostgreSQL, Amazon Aurora).
  - For other secrets (e.g., API keys or tokens), use Lambda for customized rotation functions.

---

### <span style="color:green">AWS Shield</span>
- **Description:** Managed Distributed Denial of Service (DDoS) protection service.
- **Protection Levels:**
  - **AWS Shield Standard:** Automatic and free DDoS protection for CloudFront and Route 53 resources.
  - **AWS Shield Advanced:** Paid service for enhanced DDoS protection for EC2, ELB, CloudFront, and Route 53 resources.

---

### <span style="color:green">AWS WAF</span>
- **Description:** Web Application Firewall protects web applications against common web exploits.
- **Protection Levels:**
  - **Layer 7 (HTTP):** Protects against common attack patterns, such as SQL injection or Cross-site scripting (XSS).
  - **Deployment:** Can be deployed on CloudFront, Application Load Balancer, API Gateway, and AWS AppSync.

---

Here's the information formatted in Markdown with color:

---

### <span style="color:green">AWS Firewall Manager</span>
- **Description:** Centrally configure and manage AWS WAF rules, AWS Shield Advanced, Network Firewall rules, and Route 53 DNS Firewall Rules across accounts and resources in an AWS Organization.
- **Use Case:** Meet government regulations by deploying AWS WAF rules to block traffic from embargoed countries across accounts and resources.

---

### <span style="color:green">AWS GuardDuty</span>
- **Description:** Monitors VPC Flow Logs, DNS Logs, and CloudTrail events. Uses machine learning algorithms and anomaly detection to identify threats.
- **Features:** Can protect against cryptocurrency attacks.

---

### <span style="color:green">Amazon Inspector</span>
- **Description:** Automated security assessment service for EC2 instances by installing an agent on the instance OS.
- **Rules Packages:**
  - **Network Reachability:** Checks for unintended network accessibility of EC2 instances.
  - **Host Assessment:** Checks for vulnerabilities and insecure configurations, including Common Vulnerabilities and Exposures (CVE), Center for Internet Security (CIS) Operating System configuration benchmarks, and security best practices.

---

### <span style="color:green">Amazon Macie</span>
- **Description:** Managed service to discover and protect sensitive data in AWS.
- **Features:** Identifies and alerts on sensitive data, such as Personally Identifiable Information (PII) in selected S3 buckets.

---

### <span style="color:green">AWS Config</span>
- **Description:** Managed service to assess, audit, and evaluate configurations of AWS resources across multiple regions and accounts.
- **Features:**
  - Notifies via SNS for any configuration changes.
  - Integrated with CloudTrail to provide resource configuration history.
- **Use Case:** Assesses compliance with standards like PCI-DSS (Payment Card Industry Data Security Standard) or HIPAA (U.S. Health Insurance Portability and Accountability Act).

---

Feel free to adjust any details as needed! 