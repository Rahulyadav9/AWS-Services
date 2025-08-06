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
