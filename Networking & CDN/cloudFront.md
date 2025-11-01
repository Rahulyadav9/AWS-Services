

## 🌍 **AWS CDN (CloudFront) INTERVIEW QUESTIONS**

### **21. What is Amazon CloudFront?**

**Amazon CloudFront** is a **Content Delivery Network (CDN)** that delivers content (web pages, videos, APIs) globally using **edge locations** to reduce latency and improve performance.

---

### **22. How does CloudFront work?**

1. A user requests content via DNS.
2. CloudFront routes it to the **nearest edge location**.
3. If cached → Served instantly.
4. If not cached → Fetched from **origin (S3, EC2, or ALB)** and cached.

---

### **23. What are CloudFront edge locations?**

Edge locations are **data centers** located globally where CloudFront caches content to serve it closer to users.

---

### **24. What is an Origin in CloudFront?**

The **origin** is the **source of content** that CloudFront distributes.
Examples:

* S3 bucket
* EC2 instance
* Elastic Load Balancer
* Custom HTTP server

---

### **25. What is TTL (Time To Live) in CloudFront?**

**TTL** determines how long content remains cached at an edge location before CloudFront revalidates it from the origin.

---

### **26. What are CloudFront behaviors?**

Behaviors control how CloudFront handles requests, including:

* Cache policy
* Viewer protocol (HTTP/HTTPS)
* Origin request policy
* Redirects or caching rules based on paths (`/images/*`, `/api/*`)

---

### **27. What is the difference between S3 and CloudFront?**

| Feature         | S3                      | CloudFront              |
| --------------- | ----------------------- | ----------------------- |
| Purpose         | Object storage          | Content delivery        |
| Caching         | ❌ No                    | ✅ Yes                   |
| Global presence | Regional                | Global (edge locations) |
| Latency         | Higher                  | Lower                   |
| HTTPS support   | Yes (via bucket policy) | Yes (via SSL certs)     |

---

### **28. How do you restrict CloudFront access to S3?**

Use **Origin Access Control (OAC)** or older **Origin Access Identity (OAI)** to restrict direct S3 access and only allow requests from CloudFront.

---

### **29. What is signed URL vs signed cookie in CloudFront?**

| Type              | Description                     | Use Case                           |
| ----------------- | ------------------------------- | ---------------------------------- |
| **Signed URL**    | Grants access to a single file  | Private video or image             |
| **Signed Cookie** | Grants access to multiple files | Streaming sites or multiple assets |

---

### **30. What is Lambda@Edge?**

**Lambda@Edge** allows you to run **serverless functions** at CloudFront edge locations to modify content or headers before delivering to users — without managing servers.

Example use cases:

* Redirects based on country/language
* Header injection
* Authentication at the edge

---

### **31. What is AWS Global Accelerator vs CloudFront?**

| Feature   | CloudFront                 | Global Accelerator        |
| --------- | -------------------------- | ------------------------- |
| Type      | CDN (Content Delivery)     | Network layer accelerator |
| Use Case  | Static/dynamic web content | API, TCP/UDP apps         |
| Caching   | Yes                        | No                        |
| Protocols | HTTP/HTTPS                 | TCP/UDP                   |

---

## 🧠 **SCENARIO-BASED QUESTIONS**

### **32. You want to host a web app that’s globally available and low-latency. How?**

* Host backend in **EC2/ECS**
* Store static content in **S3**
* Use **CloudFront** to cache globally
* Use **Route 53** for DNS

---

### **33. You want a private app that connects to S3 without using the internet.**

Use an **S3 VPC Endpoint (Gateway type)** — connects privately to S3.

---

### **34. You need to securely connect multiple VPCs across regions.**

Use **Transit Gateway** (hub-and-spoke) or **VPC Peering** (for few VPCs).

---

### **35. How do you handle DDoS protection in AWS?**

* **AWS Shield** (Standard or Advanced)
* **WAF** (Web Application Firewall)
* **CloudFront** (absorbs edge attacks)
* **Route 53** (DNS-level protection)

---

### **36. You want to stream live video globally. How?**

* Store stream in **S3**
* Distribute via **CloudFront**
* Use **Signed URLs** for secure access
* Optionally, use **MediaConvert / MediaLive**

---

## 🧩 **BONUS: KEY AWS NETWORKING SERVICES OVERVIEW**

| Service                | Description                  |
| ---------------------- | ---------------------------- |
| **VPC**                | Isolated virtual network     |
| **Route 53**           | DNS service                  |
| **CloudFront**         | CDN for content delivery     |
| **Direct Connect**     | Dedicated on-premises link   |
| **VPN**                | Secure internet connection   |
| **Transit Gateway**    | Central VPC hub              |
| **PrivateLink**        | Private service connectivity |
| **Global Accelerator** | Global network optimization  |

---

Would you like me to create a **visual cheat sheet (PDF)** showing:

* AWS networking diagram (VPC, subnets, NAT, IGW)
* CloudFront flow
* Difference between TGW, VPC Peering, and PrivateLink
  It’s ideal for **interview prep or certification revision (SAA / DevOps Pro)**.
