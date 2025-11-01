| Service                                  | Description                        |
| ---------------------------------------- | ---------------------------------- |
| **IAM (Identity and Access Management)** | User/role/permissions management   |
| **Cognito**                              | User sign-up/login/authentication  |
| **KMS (Key Management Service)**         | Encryption key management          |
| **Secrets Manager**                      | Securely store credentials/secrets |


Here’s a **complete AWS IAM (Identity and Access Management) interview Q&A guide** — from **basic to advanced**, including **real-world examples and scenario-based questions** 👇

---

## 🧩 **BASIC AWS IAM INTERVIEW QUESTIONS**

### **1️⃣ What is AWS IAM?**

**AWS IAM (Identity and Access Management)** is a service that helps you **securely control access** to AWS resources.
It enables you to manage **who** can access (users, groups, roles) and **what** they can do (permissions, policies).

---

### **2️⃣ What are the main components of IAM?**

| Component    | Description                                             |
| ------------ | ------------------------------------------------------- |
| **Users**    | Individuals who need access to AWS resources.           |
| **Groups**   | Collections of users with common permissions.           |
| **Roles**    | Temporary access permissions for AWS services or users. |
| **Policies** | JSON documents that define permissions.                 |

---

### **3️⃣ What is an IAM Policy?**

An **IAM Policy** is a **JSON document** that defines **permissions** (Allow/Deny) for actions on AWS resources.
Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::mybucket"
  }]
}
```

---

### **4️⃣ What are the types of IAM policies?**

1. **AWS Managed Policies** – Created and maintained by AWS.
2. **Customer Managed Policies** – Created by you for custom permissions.
3. **Inline Policies** – Attached directly to a single user, group, or role.

---

### **5️⃣ What is the difference between IAM users and IAM roles?**

| Feature     | IAM User                                      | IAM Role                         |
| ----------- | --------------------------------------------- | -------------------------------- |
| Access Type | Long-term credentials (password, access keys) | Temporary credentials            |
| Usage       | Human users                                   | AWS services, federated users    |
| Example     | Developer logging into AWS console            | EC2 instance accessing S3 bucket |

---

### **6️⃣ What are IAM Groups?**

IAM Groups are **collections of IAM users** that share the same permissions.
→ Easier to manage users (attach a policy to group instead of individuals).

---

### **7️⃣ What is the root account in AWS?**

* The **first account created** when you sign up for AWS.
* Has **full administrative privileges** over all resources.
  ✅ Should **not** be used for daily tasks — only for critical operations.

---

### **8️⃣ What are IAM Roles used for?**

* Allow **AWS services** or **external users** to assume a set of permissions temporarily.
  **Example:**
* EC2 instance assuming an IAM Role to access S3.
* Lambda function writing logs to CloudWatch.

---

### **9️⃣ What is the IAM Policy Simulator?**

A tool provided by AWS to **test and debug IAM policies** before applying them, ensuring permissions work as expected.

---

### **🔟 What are AWS Managed Policies?**

These are **predefined policies created by AWS** for common use cases like `AmazonS3FullAccess` or `AmazonEC2ReadOnlyAccess`.

---

## ⚙️ **INTERMEDIATE IAM INTERVIEW QUESTIONS**

### **11️⃣ What is the principle of least privilege?**

Give users **only the permissions they need** to perform their tasks — nothing more.

---

### **12️⃣ What is policy evaluation logic in IAM?**

AWS uses the following evaluation logic:

1. **Explicit Deny** → Overrides everything.
2. **Explicit Allow** → Grants access (if no Deny).
3. **Implicit Deny** → Default state (no permissions = deny).

---

### **13️⃣ What is an IAM Role trust policy?**

A **trust policy** defines **who can assume a role** (e.g., EC2 service, another account, or federated user).

Example:

```json
{
  "Effect": "Allow",
  "Principal": { "Service": "ec2.amazonaws.com" },
  "Action": "sts:AssumeRole"
}
```

---

### **14️⃣ How does IAM integrate with other AWS services?**

IAM integrates with almost every AWS service to manage permissions, such as:

* S3 (access control)
* EC2 (instance roles)
* Lambda (execution roles)
* CloudFormation (stack permissions)

---

### **15️⃣ How do IAM roles differ from Resource-based policies?**

| Feature     | IAM Role                | Resource-Based Policy                  |
| ----------- | ----------------------- | -------------------------------------- |
| Attached To | Identity (user/service) | Resource (S3, SNS, SQS)                |
| Access      | Temporary credentials   | Directly grants access                 |
| Example     | EC2 → S3 role           | S3 bucket allowing account B to access |

---

### **16️⃣ What is STS (AWS Security Token Service)?**

**STS** issues **temporary credentials** for IAM roles or federated users.
Example: An external application accessing AWS via a temporary session token.

---

### **17️⃣ How to provide cross-account access in AWS?**

Use **IAM Roles** with a **trust policy** that allows users from another AWS account to assume that role.

---

### **18️⃣ What is the difference between a Service Role and a Service-Linked Role?**

| Type                    | Description                                                                               |
| ----------------------- | ----------------------------------------------------------------------------------------- |
| **Service Role**        | A role that you create and assign to an AWS service (e.g., EC2 role).                     |
| **Service-Linked Role** | Created automatically by AWS services for specific functionality (e.g., AWS Config role). |

---

### **19️⃣ How can you enforce MFA (Multi-Factor Authentication)?**

Use an IAM policy condition:

```json
"Condition": {
  "Bool": { "aws:MultiFactorAuthPresent": "true" }
}
```

This ensures access is only allowed when MFA is enabled.

---

### **20️⃣ What is IAM Access Analyzer?**

A tool that helps **detect and review resource-sharing risks**, such as S3 buckets or IAM roles shared with external accounts.

---

## 🔐 **ADVANCED IAM INTERVIEW QUESTIONS**

### **21️⃣ What is IAM Permission Boundary?**

A **permission boundary** is an **upper limit** on the permissions that an IAM user or role can have — even if other policies allow more.
Useful for controlling delegated admin access.

---

### **22️⃣ What is the difference between SCP (Service Control Policy) and IAM Policy?**

| Feature | IAM Policy         | SCP                      |
| ------- | ------------------ | ------------------------ |
| Scope   | Specific user/role | Entire AWS account or OU |
| Used In | IAM                | AWS Organizations        |
| Purpose | Grant permissions  | Restrict permissions     |

---

### **23️⃣ How can you restrict IAM user access to a specific region?**

Use a **policy condition**:

```json
"Condition": {
  "StringEquals": { "aws:RequestedRegion": "us-east-1" }
}
```

---

### **24️⃣ How to audit IAM permissions in AWS?**

Use:

* **IAM Access Advisor**
* **IAM Credential Report**
* **CloudTrail** (logs all API calls)
* **Access Analyzer**

---

### **25️⃣ How can temporary credentials be generated for IAM roles?**

Through the **AWS STS service**, using APIs like:

* `AssumeRole`
* `GetSessionToken`
* `AssumeRoleWithSAML`
* `AssumeRoleWithWebIdentity`

---

### **26️⃣ What is Identity Federation in IAM?**

Allows users from **external identity providers (IdPs)** (like Google, Okta, Active Directory) to access AWS resources using **temporary credentials** instead of creating IAM users.

---

### **27️⃣ What are IAM Condition Keys?**

Used in policies to **control access based on context**, such as:

* IP address: `"aws:SourceIp": "203.0.113.0/24"`
* Time: `"aws:CurrentTime"`
* MFA: `"aws:MultiFactorAuthPresent"`

---

### **28️⃣ What is the difference between IAM and Cognito?**

| Feature     | IAM                                 | Amazon Cognito                          |
| ----------- | ----------------------------------- | --------------------------------------- |
| Purpose     | Access management for AWS resources | User authentication for web/mobile apps |
| Users       | Admins, developers                  | End users (app users)                   |
| Credentials | Long/temporary AWS keys             | JWT tokens (OAuth2, OpenID)             |

---

## 🧠 **SCENARIO-BASED QUESTIONS**

### **29️⃣ Scenario:**

Your EC2 instance needs access to an S3 bucket — how do you set it up?

✅ **Solution:**

* Create an **IAM Role** with `AmazonS3ReadOnlyAccess` policy.
* Attach the role to the **EC2 instance**.
* EC2 automatically receives temporary credentials to access S3.

---

### **30️⃣ Scenario:**

You want to prevent a developer from deleting an S3 bucket but still allow uploads.

✅ **Solution:**
Create a **custom policy**:

```json
{
  "Effect": "Deny",
  "Action": "s3:DeleteBucket",
  "Resource": "arn:aws:s3:::mybucket"
}
```

Attach to the developer’s IAM user or group.

---

### **31️⃣ Scenario:**

You want to allow a user to manage only EC2 instances in `us-east-1`.

✅ **Solution:**
Use condition:

```json
"Condition": {
  "StringEquals": { "aws:RequestedRegion": "us-east-1" }
}
```

---

### **32️⃣ Scenario:**

You notice unused IAM users — how do you identify and remove them?

✅ **Solution:**

* Generate **IAM Credential Report**
* Check **Last Used Date**
* Disable unused users
* Delete if inactive for long periods

---

## 🧾 **SUMMARY CHEATSHEET**

| Concept             | Description                         |
| ------------------- | ----------------------------------- |
| IAM                 | Manage who can access AWS resources |
| User                | Individual identity                 |
| Group               | Collection of users                 |
| Role                | Temporary permissions               |
| Policy              | JSON permission document            |
| STS                 | Temporary credential service        |
| SCP                 | Restrict permissions across AWS Org |
| Permission Boundary | Max limit on IAM permissions        |

---

Would you like me to create a **PDF IAM Cheat Sheet** (with diagram showing User → Role → Policy → Resource flow)?
It’s great for **interview quick revision or certification prep (SAA, DevOps Pro)**.
