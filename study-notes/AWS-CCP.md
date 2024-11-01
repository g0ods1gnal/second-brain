# 1 - Cloud Concepts and Fundamentals
~~No notes taken here.~~

---

# 2 - Security and Compliance


## Identity and Access Management (IAM)
- Service used to securely control access to your AWS resources
- Controls authentication (who) and authorization (what)


## IAM Identity Center (formerly SSO)
- Allows single login across all AWS accounts (leverages AWS Organizations)
- Cloud-based apps like Salesforce, Box and Microsoft 365.
- EC2 instances running Windows
- SAML 2.0-enabled applications
- Can use multiple identity providers, such as AD, Okta, built-in IAM store, etc


## IAM Users
**Best Practices**
- Always work in your IAM account, not the root account.
    - Set up IAM users with least number of permissions needed
- Don't create access keys for the root account (delete if you have them)


## IAM User Groups
Obviously, a collection of users with certain policies applied.


## IAM Roles
- Similar to a user (an identity with permissions)
- **Does not have credentials** (passwords or keys)
- **Assumable**, **temporarily**, by anyone who needs it


## IAM Policies
**Who** can **do what** to **which resources** and **when**

Basic Syntax of a Policy:
```json
{
    "Statement": [
        {
            "Effect": "effect",
            "Action": "action",
            "Resource": "arn",
            "Condition": {
                "condition": {
                    "key": "value"
                }
            }
        }
    ]
}
```
**Effect -** Allow or Deny (default)
**Action -** The API calls to AWS services (ex: `s3:DeleteBucket`)
**Resource -** Amazon Resource Name (ARN), The resource name you want to apply permission to (ex: `arn:aws:ec2:*:*:instance/instance-id`)
**Condition -** (Optional) Control when the policy is in effect (ex: `{ "StringEquals" : { "aws:username" : "johndoe" }}`)

Example Policy:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        "Effect": "Allow",
        "Action": [
            "ec2:StartInstances",
            "ec2:StopInstances"
        ],
        "Resource": "arn:aws:ec2:*:*:instance/*",
        "Condition": {
            "StringEquals": {
                "aws:ResourceTag/Owner": "${aws:username}"
            }
        },
        {
            "Effect": "Allow",
            "Action": "ec2:DescribeInstances",
            "Resource": "*"
        }
    ]
}
```


## Multi-Factor Authentication (MFA)
- Two or more "factors" in order to authenticate
    - Something you know (ex. password)
    - Something you have (ex. phone or a hardware token)
    - Something you are (ex. fingerprint)

- Three Types of MFA Devices
    - Virtual MFA device (ex. Google Authenticator, Microsoft, etc)
    - U2F security key (ex. YubiKey)
    - Other hardware MFA device (ex. Gemalto)

**Best Practice**
- Enable MFA for your root account.


## Access Keys
- Used to send calls to AWS programmatically.
- You can have a minimum of two access keys per user. (active or inactive)


## IAM: Best Practices
- Use an IAM user for day-to-day work, NOT the root account.
- Use roles to give permissions to AWS services.
- Don't share credentials.
- Assign permissions to groups rather than to individual users.
- When assigning permissions (policies), give the least amount possible.
- Enforce MFA and strong password policies.
- Use the IAM Credentials report to audit permissions.



## Security and Compliance Services
- **Infrastructure Protection:** AWS Shield
- **Infrastructure Protection:** AWS Web Application Firewall (WAF)
- **Data Protection:** AWS Key Management System (KMS) and CloudHSM
- **Data Protection:** AWS Certificate Manager (ACM)
- **Data Protection:** AWS Secrets Manager
- **Data Protection:** Amazon Macie
- **Detection:** Amazon Inspector
- **Detection:** Amazon GuardDuty
- **Detection:** AWS Config
- **Detection:** AWS Security Hub
- **Incident Response:** Amazon Detective
- **Compliance:** AWS Artifact


### AWS Shield
- Helps prevent DDoS attacks.
- There are two types of AWS Shield:
    - **Standard -** Free, automatically protects all AWS customers.
    - **Advanced -** Paid, protects agains more sophisticated attacks, integrates with other services like CloudFront, Route 53 and Elastic Load Balancing. Also, AWS Web Application Firewall (WAF) included at no extra costs.


### AWS Web Application Firewall (WAF)
- Configure rules
    - Allow, block, monitor/count
    - IP addresses, country of origin, presence of a script, URL strings, etc


### AWS Key Management Service (KMS)
- There are two types of important encryption:
    **At Rest:** Data that's stored or archived on a device
    **In Transit:** Data being transfered from one location to another

- KMS is the primary service for encryption in AWS.
- AWS manages the encryption hardware, software and keys for you.
- Integrates with many AWS services, including EBS, S3, Redshift and CloudTrail
- FIPS 140-2 Compliance: Level 2 overall


### AWS CloudHSM
- AWS provisions the hardware and you do everything else.
    - AWS cannot access your keys
    - AWS cannot recover your keys
- Integration with other services is limited
- FIPS 140-2 Compliance: Level 3 (considered more secure)

#### Types of Keys
- **AWS Managed:** AWS creates and manages. Used by AWS services (lambda, cloud9, s3)
- **Customer Managed:** You create and manage. Can create policies to rotate keys. Specify who can use and manage the keys. Supports "bring your own key"
- **Custom Key Stores:** Created with CloudHSM. You own and manage.


### AWS Certificate Manager (ACM)
- Provision, manage and deploy public and private SSL/TLS certificates
    - Public = for resources on the public internet (these are free)
    - Private = for resources on private networks
- Loads certificates on:
    - API Gateway
    - Elastic Load Balancers
    - CloudFront distributions


### AWS Secrets Manager
The recommended way to protect secrets needed by your applications and services.


### Amazon Macie
- Works specifically with Amazon S3.
- Automatically takes an inventory of the S3 buckets and identifies and analyzes PII data using machine learning and pattern matching.
- Uses findings to automate workflows and remediation (CloudWatch + EventBridge)


### Amazon Inspector
- Automatically detects and scans for software vulnerabilities and network exposure.
- Makes sense of the findings and assigns a risk score.
- Can integrate with SecurityHub and EventBridge for workflow automation and ticketing.


### Amazon GuardDuty
- Continuously analyzes network, account and data access.
- Using machine learning, identifies and prioritizes potential threats.
- Integrates with services for further automation of workflows and remediation.


### AWS Config
- Inventory, record and audit the configuration of your AWS resources.






---
