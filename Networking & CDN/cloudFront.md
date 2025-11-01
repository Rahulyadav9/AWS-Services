Here’s a **complete AWS Networking & CDN interview Q&A guide** — covering **VPC, subnets, routing, security, and CloudFront (CDN)** — structured from **basic to advanced** with **real-world scenarios** 👇

---

## 🧩 **BASIC AWS NETWORKING CONCEPTS**

### **1. What is Amazon VPC?**

Amazon **VPC (Virtual Private Cloud)** allows you to launch AWS resources inside a **logically isolated virtual network** that you define.
You control IP addressing, routing, and network security — just like an on-premises data center network.

---

### **2. What are key components of a VPC?**

* **Subnets** – Divide your VPC into smaller networks (public/private).
* **Route Tables** – Define routing rules for subnets.
* **Internet Gateway (IGW)** – Enables internet access for public subnets.
* **NAT Gateway** – Allows private subnets to access the internet securely.
* **Security Groups (SGs)** – Instance-level firewalls.
* **Network ACLs (NACLs)** – Subnet-level firewalls.
* **Elastic IPs (EIPs)** – Static public IPs.
* **VPC Peering / Transit Gateway** – Connects VPCs together.

---

### **3. What is a Subnet?**

A **Subnet** is a range of IP addresses within a VPC.

* **Public subnet:** Has a route to an Internet Gateway.
* **Private subnet:** No direct route to the internet.

---

### **4. What is a CIDR block?**

CIDR (Classless Inter-Domain Routing) defines an IP address range, e.g.:

* **VPC CIDR:** `10.0.0.0/16`
* **Subnet CIDR:** `10.0.1.0/24`
  The `/16` or `/24` indicates how many IP addresses are available.

---

### **5. What is an Internet Gateway (IGW)?**

An **IGW** is a horizontally scaled, redundant AWS-managed gateway that allows instances in **public subnets** to connect to the Internet.

---

### **6. What is a NAT Gateway?**

A **NAT Gateway** allows instances in **private subnets** to initiate outbound connections to the internet but prevents inbound connections.

Example:

> Private EC2 → NAT Gateway → Internet

---

### **7. What is a Route Table?**

A **Route Table** contains routing rules (routes) that determine where network traffic is directed.

Example route:

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

---

### **8. Difference between Security Groups and Network ACLs?**

| Feature  | Security Group                       | Network ACL                  |
| -------- | ------------------------------------ | ---------------------------- |
| Level    | Instance-level                       | Subnet-level                 |
| Stateful | ✅ Yes                                | ❌ No                         |
| Rules    | Allow only                           | Allow & Deny                 |
| Default  | Deny all inbound, allow all outbound | Allow all inbound & outbound |

---

### **9. What is Elastic IP?**

A **static, public IPv4 address** that you can assign to an EC2 instance, NAT Gateway, or Load Balancer — remains constant even after reboot/restart.

---

### **10. What is a VPC Peering connection?**

A **network connection between two VPCs** that allows resources to communicate using private IPs.
Note: Peering does **not support transitive routing**.

---

## ⚙️ **INTERMEDIATE NETWORKING QUESTIONS**

### **11. What is AWS Transit Gateway?**

A **Transit Gateway (TGW)** acts as a **central hub** to connect multiple VPCs, VPNs, and on-premises networks.
It simplifies complex network topologies.

---

### **12. What is the difference between VPC Peering and Transit Gateway?**

| Feature            | VPC Peering | Transit Gateway |
| ------------------ | ----------- | --------------- |
| Type               | One-to-one  | Hub-and-spoke   |
| Transitive Routing | ❌ No        | ✅ Yes           |
| Scalability        | Limited     | Highly scalable |
| Cost               | Cheaper     | More expensive  |

---

### **13. What is AWS Direct Connect?**

**Direct Connect** provides a **dedicated physical network connection** from your on-premises data center to AWS, for **low latency** and **high throughput**.

---

### **14. What is a VPN connection in AWS?**

A **VPN (Virtual Private Network)** connects your on-premises network to AWS VPC using the **Internet**, providing **encrypted connectivity**.

---

### **15. What is a VPC Endpoint?**

A **VPC Endpoint** enables private connections between your VPC and AWS services without using the internet.
Two types:

* **Interface Endpoint (ENI-based)**
* **Gateway Endpoint (S3/DynamoDB)**

---

### **16. What are Elastic Network Interfaces (ENI)?**

ENIs are **virtual network cards** that can be attached to EC2 instances.
They contain IPs, MACs, and security groups.

---

### **17. What is an AWS PrivateLink?**

**PrivateLink** allows private connectivity between VPCs, services, and on-premises applications without exposing traffic to the public Internet.

---

### **18. What are IPv4 and IPv6 in AWS VPC?**

AWS supports **dual-stack networking**, meaning both IPv4 (`10.0.0.0/16`) and IPv6 (`2406:da1:...`) can be used in a VPC for broader addressability.

---

### **19. What is a Bastion Host (Jump Box)?**

A **bastion host** is an EC2 instance in a **public subnet** used to securely access instances in **private subnets** via SSH.

---

### **20. How can you connect multiple AWS accounts securely?**

* **Transit Gateway**
* **PrivateLink**
* **VPC Peering**
* **AWS Organizations + SCPs**

---

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
