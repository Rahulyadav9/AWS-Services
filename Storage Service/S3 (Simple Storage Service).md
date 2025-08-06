
# Amazon S3 (Simple Storage Service) - Notes

Amazon S3 is a highly scalable, secure, and durable object storage service provided by AWS. It allows users to store and retrieve any amount of data from anywhere on the web.

---

## 1. Buckets

* A **bucket** is a container for storing objects.
* Bucket names must be **globally unique**.
* You must specify an AWS Region when creating a bucket.
* Supports **versioning**, **encryption**, **logging**, and **policies**.

## 2. Objects

* An **object** is a file and metadata stored in a bucket.
* Each object has:

  * **Key** (the name used to identify the object)
  * **Value** (the content/data)
  * **Metadata** (optional, user-defined or system-defined)
  * **Version ID** (if versioning is enabled)

## 3. Storage Classes

| Class                   | Use Case                                   |
| ----------------------- | ------------------------------------------ |
| S3 Standard             | Frequent access data                       |
| S3 Intelligent-Tiering  | Automatic tiering based on access patterns |
| S3 Standard-IA          | Infrequent access with fast retrieval      |
| S3 One Zone-IA          | Infrequent access in a single AZ           |
| S3 Glacier              | Archive, retrieval in minutes to hours     |
| S3 Glacier Deep Archive | Long-term archive, retrieval in hours      |

## 4. Security and Access

* **IAM Policies**: User/role-based access control
* **Bucket Policies**: Set access rules at the bucket level
* **Access Control Lists (ACLs)**: Object-level permissions
* **S3 Block Public Access**: Global setting to prevent public access
* **Encryption**: SSE-S3, SSE-KMS, SSE-C, Client-Side Encryption

## 5. Key Features

* **Versioning**: Keeps multiple versions of objects
* **Lifecycle Rules**: Auto-transition or delete based on age
* **Static Website Hosting**: Serve static websites directly
* **Replication**: Cross-Region or Same-Region replication
* **Event Notification**: Trigger events on object changes
* **CORS Configuration**: Manage cross-origin access

## 6. Operations

### AWS CLI Commands:

```bash
# Upload a file
aws s3 cp myfile.txt s3://my-bucket/

# Download a file
aws s3 cp s3://my-bucket/myfile.txt .

# Sync a folder
aws s3 sync ./local-folder s3://my-bucket/
```

### SDK Example (Node.js):

```js
const AWS = require('aws-sdk');
const s3 = new AWS.S3();

const params = {
  Bucket: 'my-bucket',
  Key: 'example.txt',
  Body: 'Hello World'
};

s3.putObject(params, function(err, data) {
  if (err) console.error(err);
  else console.log("Successfully uploaded!");
});
```

## 7. Best Practices

* Enable **versioning** and **MFA delete**.
* Use **lifecycle rules** to manage costs.
* Avoid **public buckets** unless necessary.
* Use **CloudFront** for CDN distribution.
* Monitor usage with **CloudWatch** and enable **S3 Access Logs**.
* Always encrypt sensitive data.

---

Amazon S3 is a powerful tool for scalable and reliable data storage in the cloud. It is widely used in hosting websites, backup systems, big data analytics, and more.



I’ll break this into **simple, clear steps**, covering:
✅ Bucket policies
✅ IAM policies
✅ ACLs
✅ Block Public Access

---

## 🎯 1️⃣ Bucket Policies

**Bucket Policies** are JSON documents attached to a bucket to control access at the bucket level.

**How to add a bucket policy:**

1. Go to **AWS S3 Console**.
2. Select your bucket.
3. Go to the **Permissions** tab.
4. Choose **Bucket Policy**.
5. Add a JSON policy. For example:

   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::your-bucket-name/*"
       }
     ]
   }
   ```

   * This makes **all objects publicly readable**.
   * Be careful—**this can expose data publicly**.

✅ Use the **Policy Generator** link in the console to help create policies.

---

## 🎯 2️⃣ IAM Policies

**IAM Policies** attach to users, groups, or roles and define what actions they can perform on buckets.

**Example IAM policy to allow listing and reading objects:**

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ]
    }
  ]
}
```

Attach this policy to an IAM user or role via the **IAM Console**.

---

## 🎯 3️⃣ Access Control Lists (ACLs)

ACLs are a legacy way to control permissions **per object** or **per bucket**.

**Common usage:**

* Grant read access to everyone (`AllUsers`).
* Grant access to specific AWS accounts.

**How to set ACLs:**

1. In S3 console, go to the bucket or object.
2. Click **Permissions > Access Control List**.
3. Add grantees and select permissions (Read, Write).

---

## 🎯 4️⃣ Block Public Access

AWS provides a **Block Public Access** setting to prevent accidental exposure.

**Recommendation:**
✅ Enable **Block all public access** unless you explicitly need to make content public.

**How to configure:**

1. Go to your bucket.
2. In **Permissions**, choose **Block Public Access**.
3. Enable or disable as needed.

---

## ✅ Quick Tips:

* Prefer **IAM policies** for internal access control.
* Use **bucket policies** for public access or cross-account permissions.
* Be careful with ACLs—they are harder to manage.
* Always **test your configuration** using the **S3 Access Analyzer**.
* If you need temporary credentials, use **pre-signed URLs**.

---


