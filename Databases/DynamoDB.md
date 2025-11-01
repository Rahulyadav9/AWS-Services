| Service                               | Description                                              |
| ------------------------------------- | -------------------------------------------------------- |
| **RDS (Relational Database Service)** | Managed SQL DBs (MySQL, PostgreSQL, etc.)                |
| **DynamoDB**                          | NoSQL database                                           |
| **Aurora**                            | High-performance SQL DB compatible with MySQL/PostgreSQL |
| **ElastiCache**                       | In-memory caching (Redis/Memcached)                      |




Here’s a **comprehensive DynamoDB interview Q&A guide** — from **basic to advanced**, with real-world use cases and scenario-based questions — ideal for backend, AWS, or full-stack developer interviews 👇

---

## 🧩 **Basic DynamoDB Interview Questions**

### **1. What is Amazon DynamoDB?**

Amazon **DynamoDB** is a **fully managed NoSQL database service** provided by AWS that offers **fast and predictable performance with seamless scalability**. It stores data in **key-value and document formats**.

---

### **2. What are the key features of DynamoDB?**

* Fully managed (no servers to manage)
* High availability (multi-AZ replication)
* Scales automatically (on-demand mode)
* Low latency (typically single-digit milliseconds)
* Integrated **backup, restore**, and **streams**
* Supports **transactions**, **TTL**, and **Global Tables**

---

### **3. What are DynamoDB’s primary data models?**

1. **Tables** – Container for data.
2. **Items** – A record (like a row in RDBMS).
3. **Attributes** – Data fields within an item (like columns).

---

### **4. What is a Primary Key in DynamoDB?**

The **primary key** uniquely identifies each item in a table.
It can be of two types:

1. **Partition Key only (Simple Primary Key)** → e.g., `userId`
2. **Partition + Sort Key (Composite Primary Key)** → e.g., `userId + orderDate`

---

### **5. What is a Partition Key?**

A **Partition Key** is used to determine the partition (physical location) where data is stored.
All items with the same partition key are stored together.

---

### **6. What is a Sort Key?**

When a **Sort Key** is added, items with the same Partition Key can be **sorted** and queried efficiently by the Sort Key.

Example:

| userId | orderDate  | amount |
| ------ | ---------- | ------ |
| 101    | 2024-01-01 | 500    |
| 101    | 2024-02-01 | 700    |

Here, `userId` = Partition Key, `orderDate` = Sort Key.

---

### **7. What is the difference between DynamoDB and RDS?**

| Feature      | DynamoDB            | RDS                          |
| ------------ | ------------------- | ---------------------------- |
| Type         | NoSQL               | SQL                          |
| Schema       | Schema-less         | Fixed schema                 |
| Scaling      | Automatic           | Manual (vertical/horizontal) |
| Query Type   | Key-based queries   | Complex SQL joins            |
| Transactions | Supported (limited) | Fully supported              |
| Cost Model   | Per request         | Per instance/hour            |

---

### **8. What is a Secondary Index in DynamoDB?**

A **Secondary Index** allows you to query data using **non-primary key attributes**.

Types:

* **Local Secondary Index (LSI)** – Same partition key, different sort key.
* **Global Secondary Index (GSI)** – Different partition and sort keys.

---

## ⚙️ **Intermediate DynamoDB Interview Questions**

### **9. What is a Local Secondary Index (LSI)?**

* Created at table creation time.
* Shares the same **partition key** as the base table.
* Has a **different sort key**.
* Max **5 LSIs** per table.

---

### **10. What is a Global Secondary Index (GSI)?**

* Can be created **anytime** after table creation.
* Has a **different partition and sort key**.
* Enables **faster queries** on non-key attributes.
* Uses **separate read/write capacity units (RCUs/WCUs).**

---

### **11. What are Read and Write Capacity Units (RCU/WCU)?**

| Unit    | Definition                                                  |
| ------- | ----------------------------------------------------------- |
| **RCU** | 1 strongly consistent read per second for items up to 4 KB. |
| **WCU** | 1 write per second for items up to 1 KB.                    |

---

### **12. What are the two capacity modes in DynamoDB?**

1. **Provisioned Mode** – You manually set RCU/WCU.
2. **On-Demand Mode** – DynamoDB automatically scales capacity up/down and charges per request.

---

### **13. What is DynamoDB Stream?**

* Captures changes (insert, update, delete) in table items.
* Can trigger **AWS Lambda** for real-time processing (e.g., audit logs, notifications, replication).

---

### **14. What is Time to Live (TTL)?**

TTL automatically deletes expired items from a table based on a timestamp attribute.

---

### **15. What is a Global Table in DynamoDB?**

A **Global Table** is a multi-region, fully replicated table that allows **active-active replication** across AWS regions for low-latency global access.

---

### **16. How does DynamoDB ensure high availability?**

* Data is **automatically replicated** across multiple **Availability Zones**.
* Each partition has **3 replicas** for fault tolerance.

---

### **17. How can you back up data in DynamoDB?**

* **On-demand backup** (manual snapshot)
* **Point-in-time recovery (PITR)** – Restores data to any second in the last 35 days.

---

### **18. What is the maximum item size in DynamoDB?**

* **400 KB** (including all attribute names and values).

---

### **19. What are DynamoDB Streams used for?**

To capture table activity and send changes to **Lambda**, **Kinesis**, or **another DynamoDB table**.

---

### **20. What is Query vs Scan in DynamoDB?**

| Operation | Description                                                                | Efficiency               |
| --------- | -------------------------------------------------------------------------- | ------------------------ |
| **Query** | Fetches items using **Partition Key** and optional **Sort Key condition**. | Fast                     |
| **Scan**  | Reads **every item** in the table.                                         | Slow (avoid if possible) |

---

## 🔒 **Advanced DynamoDB Interview Questions**

### **21. What are DynamoDB transactions?**

DynamoDB supports **ACID transactions** for coordinated, all-or-nothing operations across multiple items and tables.

---

### **22. How can you improve performance in DynamoDB?**

* Use **Query** instead of **Scan**.
* Use **GSIs** and **LSIs** effectively.
* Use **parallel scans** (if scan needed).
* Use **DAX (DynamoDB Accelerator)** for caching.
* Optimize **partition key** selection (avoid hot keys).

---

### **23. What is DynamoDB Accelerator (DAX)?**

**DAX** is an **in-memory caching layer** for DynamoDB that improves read performance up to **10x**.
It’s fully managed and compatible with DynamoDB API calls.

---

### **24. What is a hot partition problem?**

When a single partition key gets **too much traffic**, it becomes a bottleneck.
Fix:

* Use **composite keys**
* Add **random suffixes** to partition keys
* Use **write sharding**

---

### **25. What is Conditional Write in DynamoDB?**

Allows you to **update or delete** items only if a **condition is met**, ensuring consistency (e.g., avoid overwriting newer data).

---

### **26. What is eventual vs strong consistency in DynamoDB?**

| Type                      | Description                             | Use Case                 |
| ------------------------- | --------------------------------------- | ------------------------ |
| **Strongly Consistent**   | Returns the most recent data.           | Financial transactions   |
| **Eventually Consistent** | May return stale data for a short time. | High-read apps (default) |

---

### **27. What is the difference between BatchWriteItem and BatchGetItem?**

| API                | Purpose                                  |
| ------------------ | ---------------------------------------- |
| **BatchWriteItem** | Insert or delete up to 25 items at once. |
| **BatchGetItem**   | Retrieve up to 100 items at once.        |

---

### **28. What are reserved words in DynamoDB?**

Some attribute names (like “size”, “timestamp”) are reserved — you must use **ExpressionAttributeNames** to alias them.

---

### **29. What is optimistic locking in DynamoDB?**

Uses a **version number** to prevent overwriting concurrent updates — common in distributed systems.

---

### **30. How to implement pagination in DynamoDB?**

Use **LastEvaluatedKey** returned by queries/scans to fetch the next page of results.

---

## 🧠 **Scenario-Based Questions**

### **31. You want to store user sessions for a website. How would you design it?**

* Table: `UserSessions`
* Partition Key: `userId`
* Attributes: `sessionId`, `lastActive`, `TTL`
* Use **TTL** for automatic session expiry.

---

### **32. How would you store product catalog data with category-based queries?**

* Partition Key: `category`
* Sort Key: `productId`
* Use **GSI** for searching by product name or brand.

---

### **33. You need cross-region replication — how to do it?**

Use **Global Tables** (multi-region active-active setup).

---

### **34. You need to audit every change in the table — solution?**

Enable **DynamoDB Streams** → trigger a **Lambda** to log changes to S3 or CloudWatch.

---

### **35. How do you migrate from RDS to DynamoDB?**

* Use **AWS DMS (Database Migration Service)** for data transfer.
* Redesign schema for **NoSQL key-value model**.

---

Would you like me to create a **DynamoDB Interview PDF Cheat Sheet** (with diagrams showing partitioning, indexes, and stream flow)?
It’s great for quick revision before interviews.
