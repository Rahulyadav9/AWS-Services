
## **1. Introduction**

* **Full Form**: *Elastic Compute Cloud*
* **Definition**: Amazon EC2 is a web service that provides **resizable compute capacity** in the cloud.
* **Purpose**:

  * Run applications without owning physical servers.
  * Easily scale computing resources up or down.
* **Payment Model**: Pay-as-you-go (no upfront investment).

---

## **2. Key Features**

* **Elasticity** – Launch or terminate instances as needed.
* **Scalability** – Adjust compute resources to match workload.
* **Wide OS Support** – Linux, Windows, macOS, custom AMIs.
* **Global Reach** – Available in multiple AWS Regions & Availability Zones.
* **Instance Variety** –

  * **General Purpose**: Balanced CPU/memory (e.g., `t3`, `m5`).
  * **Compute Optimized**: High CPU performance (e.g., `c5`).
  * **Memory Optimized**: For RAM-heavy workloads (e.g., `r5`).
  * **Storage Optimized**: High disk throughput (e.g., `i3`).
  * **Accelerated Computing**: GPUs / FPGAs (e.g., `p3`, `g4`).
* **Security** – Integrated with **IAM**, **Security Groups**, and **Key Pairs**.
* **Integration** – Works with **EBS**, **S3**, **VPC**, **CloudWatch**, **Load Balancers**.

---

## **3. Pricing Models**

1. **On-Demand Instances**

   * Pay per hour/second.
   * No long-term contract.
   * Best for short-term, unpredictable workloads.

2. **Reserved Instances (RI)**

   * Commitment for 1 or 3 years.
   * Up to 72% cheaper than on-demand.
   * Best for steady workloads.

3. **Spot Instances**

   * Use spare AWS capacity at huge discounts.
   * Can be terminated by AWS anytime.
   * Best for flexible, fault-tolerant workloads.

4. **Savings Plans**

   * Commit to a certain amount of compute usage (\$/hour).
   * Flexible across instance families & regions.

---

## **4. Important Components**

* **AMI (Amazon Machine Image)**

  * Blueprint containing OS, software, and configurations.
  * Types:

    * AWS-provided
    * Marketplace
    * Custom

* **Instance Type**

  * Defines CPU, memory, storage, and networking capacity.
  * Example: `t3.micro`, `m5.large`, `c5.xlarge`.

* **Elastic IP Address**

  * Static, public IPv4 address for EC2 instances.

* **EBS (Elastic Block Store)**

  * Persistent block storage for EC2.
  * Data persists even after instance stop/terminate.

* **Security Groups**

  * Virtual firewalls controlling inbound and outbound traffic.

---

## **5. Common EC2 Lifecycle Operations**

* **Launch** – Create an instance from an AMI.
* **Connect** – SSH (Linux) or RDP (Windows) into instance.
* **Stop** – Shut down but keep EBS volumes.
* **Terminate** – Shut down and delete instance + attached volumes.
* **Reboot** – Restart instance without data loss.

---

## **6. Monitoring & Management**

* **CloudWatch** – Monitor metrics (CPU, network, disk, status checks).
* **CloudTrail** – Track API calls and changes.
* **Elastic Load Balancer (ELB)** – Distribute traffic among instances.
* **Auto Scaling** – Automatically adjust the number of instances.

---

## **7. Security Best Practices**

* Use **IAM roles** for access control.
* Enable **Security Groups** & **Network ACLs**.
* Use **Key Pairs** for SSH login.
* Regularly patch/update OS & software.
* Enable **CloudTrail** for auditing.

---

## **8. Advantages**

* On-demand scalability.
* Flexible pricing.
* Global availability.
* Tight integration with other AWS services.

## **9. Limitations**

* Requires cloud & networking knowledge.
* Costs can rise if not monitored.
* Instance termination in Spot model.

---

## **10. Example Use Cases**

* Hosting websites & APIs.
* Machine learning workloads.
* Big data processing.
* Game servers.
* CI/CD build servers.



Got it 👍
Here’s a **comprehensive EC2 interview Q&A guide** (from basics → advanced → scenario-based).

---

## 🚀 **AWS EC2 Interview Q&A**

### **1. Basics**

**Q:** What is Amazon EC2?
**A:** EC2 (Elastic Compute Cloud) is a web service that provides resizable compute capacity (virtual servers) in the cloud. You can run applications without investing in physical servers.

**Q:** What are the different types of EC2 instances?
**A:**

* **General Purpose** – Balanced (e.g., T, M family).
* **Compute Optimized** – CPU-heavy (C family).
* **Memory Optimized** – RAM-heavy (R, X family).
* **Storage Optimized** – High IOPS (I, D family).
* **Accelerated Computing** – GPU/FPGA (P, G family).

**Q:** What are EC2 pricing models?
**A:**

1. **On-Demand** – Pay per second/hour, flexible.
2. **Reserved Instances** – 1 or 3-year commitment, cheaper.
3. **Spot Instances** – Bid for unused capacity, cheapest but can be interrupted.
4. **Savings Plans** – Flexible usage commitment.
5. **Dedicated Hosts/Instances** – Physical servers for compliance.

---

### **2. Storage**

**Q:** What’s the difference between EBS and Instance Store?
**A:**

* **EBS (Elastic Block Store):** Persistent, survives stop/start.
* **Instance Store:** Temporary, data lost if instance stops/terminates.

**Q:** Types of EBS volumes?
**A:**

* gp3/gp2 (General Purpose SSD)
* io1/io2 (Provisioned IOPS SSD)
* st1 (Throughput Optimized HDD)
* sc1 (Cold HDD)

---

### **3. Networking**

**Q:** What is an Elastic IP in EC2?
**A:** A static IPv4 address that you can associate with an instance. Unlike public IPs, Elastic IPs persist across stop/start.

**Q:** What’s the difference between Security Groups and NACLs?
**A:**

* **Security Groups:** Instance-level, stateful, allow rules only.
* **NACLs:** Subnet-level, stateless, allow + deny rules.

**Q:** How do you connect to an EC2 instance?
**A:**

* Linux: SSH using `.pem` key pair.
* Windows: RDP using `.pem` + Administrator password.

---

### **4. Scaling & Load Balancing**

**Q:** What is Auto Scaling in EC2?
**A:** Automatically adjusts the number of EC2 instances based on demand. Works with CloudWatch alarms.

**Q:** How do Load Balancers work with EC2?
**A:** Elastic Load Balancer (ELB) distributes incoming traffic across multiple EC2 instances for high availability.

---

### **5. Security**

**Q:** How do you secure sensitive credentials in EC2?
**A:**

* Don’t hardcode credentials.
* Use IAM roles for EC2.
* Use AWS Systems Manager Parameter Store or Secrets Manager.

**Q:** What happens if you lose the `.pem` key for an EC2 instance?
**A:**

* Stop the instance, detach its root volume.
* Attach the volume to another instance.
* Add a new public key to the `~/.ssh/authorized_keys` file.
* Reattach and start the instance.

---

### **6. Monitoring & Troubleshooting**

**Q:** How do you monitor an EC2 instance?
**A:** Use **CloudWatch Metrics** (CPU, Network, Disk), **CloudWatch Logs**, and enable **Detailed Monitoring**.

**Q:** An EC2 instance is unreachable (can’t SSH). What steps would you take?
**A:**

1. Check Security Group (port 22 open).
2. Check NACL rules.
3. Verify correct key pair.
4. Ensure the instance has a public IP / Elastic IP.
5. Check if the OS-level firewall is blocking access.

---

### **7. Advanced / Scenario-Based**

**Q:** How do you migrate an on-premise application to EC2?
**A:**

* Use AWS **Server Migration Service (SMS)** or **Application Migration Service (MGN)**.
* Create AMIs and launch equivalent EC2 instances.

**Q:** You need **zero downtime deployment** on EC2, how would you achieve it?
**A:**

* Use **Auto Scaling Group** + **Load Balancer**.
* Deploy new version to new instances → switch traffic gradually.
* Or use **Blue/Green Deployment** with Route 53.

**Q:** Your EC2 bill is too high. What steps would you take to optimize cost?
**A:**

* Use **Reserved Instances** or **Savings Plans**.
* Use **Spot Instances** for non-critical workloads.
* Right-size instances (monitor CPU/memory).
* Turn off unused instances.

**Q:** How do you achieve high availability with EC2?
**A:**

* Launch instances across **multiple AZs**.
* Place them behind an **ELB**.
* Enable **Auto Scaling**.

**Q:** How do you back up data from EC2?
**A:**

* Create **EBS snapshots** (incremental backups).
* Use **Amazon Machine Image (AMI)** for whole-instance backup.
* Sync files to **S3**.

---
