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
- Obviously, a collection of users with certain policies applied.

## IAM Roles
- Similar to a user (an identity with permissions)
- **Does not have credentials** (passwords or keys)
- **Assumable**, **temporarily**, by anyone who needs it

## IAM Policies
- **Who** can **do what** to **which resources** and **when**

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

---
