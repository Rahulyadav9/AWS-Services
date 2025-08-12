
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

