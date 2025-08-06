# Amazon S3 Notes

Amazon S3 (Simple Storage Service) is a scalable object storage service provided by AWS. It is used to store and retrieve any amount of data from anywhere on the web.

---

## 🔹 Basic Concepts

### ✅ Bucket
- A container for storing objects (files).
- Unique name across all AWS regions.
- Created in a specific AWS region.

### ✅ Object
- The actual file/data stored in S3.
- Consists of data, metadata, and a unique key (name).

### ✅ Key
- Unique identifier for an object within a bucket (like a file path).

### ✅ Region
- S3 buckets are created in specific regions to optimize latency and costs.

---

## 🔹 Key Features

- **Durability**: 99.999999999% (11 9’s) durability.
- **Availability**: 99.99% availability (Standard class).
- **Scalability**: Automatically scales to handle large volumes.
- **Security**:
  - IAM policies
  - Bucket policies
  - ACL (Access Control List)
  - Encryption (SSE-S3, SSE-KMS, SSE-C)

---

## 🔹 Storage Classes

| Class                 | Use Case                             | Availability | Durability       |
|----------------------|--------------------------------------|--------------|------------------|
| S3 Standard          | Frequently accessed data             | 99.99%       | 99.999999999%    |
| S3 Intelligent-Tiering| Auto moves data between tiers       | 99.9–99.99%  | 99.999999999%    |
| S3 Standard-IA       | Infrequently accessed dat
