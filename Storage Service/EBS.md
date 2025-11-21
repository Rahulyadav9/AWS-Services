EBS (Elastic Block Store)

---

# 🚀 **What is AWS EBS (Elastic Block Store)?**

AWS **Elastic Block Store (EBS)** is a **block storage** service used with **EC2 instances**.
Think of it like a **virtual hard drive** attached to your EC2 VM.

You can:

* Attach/Detach volumes
* Resize
* Take Snapshots (backups)
* Encrypt volumes
* Monitor with CloudWatch

---

# 🧱 **Where EBS is used?**

* Root volume of EC2 (OS disk)
* Data disks for databases (MongoDB, MySQL, PostgreSQL)
* File systems (ext4, xfs)
* High IOPS workloads

---

# 🧩 **EBS Volume Types**

### 1️⃣ **gp3 – General Purpose SSD (Recommended)**

* Good performance
* Used for most apps
* Low cost

### 2️⃣ **gp2 – General Purpose SSD (Older)**

* Performance depends on volume size

### 3️⃣ **io2 / io2 Block Express – High Performance SSD**

* Extreme IOPS required
* Databases, OLTP, analytics

### 4️⃣ **st1 – Throughput Optimized HDD**

* Big data, logs, streaming workloads

### 5️⃣ **sc1 – Cold HDD**

* Low-cost storage for infrequent access

---

# 🛡 **EBS Snapshots**

Snapshots = Backups of EBS
Snapshots stored in S3 (internal AWS-managed space)

You can:

* Clone volumes from snapshot
* Schedule automatic backups (Data Lifecycle Manager)

---

# 📊 **Important EBS Metrics (CloudWatch)**

| Metric                             | Meaning                   |
| ---------------------------------- | ------------------------- |
| **VolumeReadOps / VolumeWriteOps** | IOPS usage                |
| **VolumeThroughputPercentage**     | Throughput used (%)       |
| **VolumeConsumedReadWriteOps**     | Burst balance (gp2 / st1) |
| **StatusCheckFailed**              | Volume is impaired        |
| **BurstBalance**                   | 0% means performance drop |

---

# 🔔 **CloudWatch Alarms for EBS (High Priority)**

## 1️⃣ **EBS Volume Health Alarm**

Triggers if the EBS volume is impaired.

**Metric:** `StatusCheckFailed`
**Condition:** > 0

## 2️⃣ **Burst Balance Alarm (Important for gp2/st1/sc1)**

If burst balance = 0, performance becomes slow.

**Metric:** `BurstBalance`
**Condition:** `< 20%`

## 3️⃣ **High Queue Length Alarm**

Queue length increases when EBS cannot handle load.

**Metric:** `VolumeQueueLength`
**Condition:** > 10

## 4️⃣ **High Throughput Alarm**

**Metric:** `VolumeThroughputPercentage`
**Condition:** > 80%

---

# 🧭 **Step-by-Step: Create EBS CloudWatch Alarm**

### **STEP 1 — Go to CloudWatch → Alarms → Create alarm**

---

### **STEP 2 — Select Metric**

Choose:

`EBS → Per-Volume Metrics → <your-volume-id>`

Common metrics:

* **BurstBalance**
* **StatusCheckFailed**
* **VolumeQueueLength**

---

### **STEP 3 — Set Threshold**

Example: EBS health alarm

```
Alarm when StatusCheckFailed > 0
for 1 data point of 5 minutes.
```

---

### **STEP 4 — Add Action (SNS Alert)**

Choose:

* Email notification
* Slack (via webhook + Lambda)
* SMS

---

### **STEP 5 — Name It**

Example:

```
EBS-Volume-Impaired-Alarm
EBS-Burst-Balance-Low
EBS-QueueLength-High
```

---

# 🧾 **CloudFormation Example — EBS Alarm (JSON)**

## **EBS Health Alarm**

```json
{
  "Resources": {
    "EBSHealthAlarm": {
      "Type": "AWS::CloudWatch::Alarm",
      "Properties": {
        "AlarmName": "EBS-Volume-Impaired",
        "MetricName": "StatusCheckFailed",
        "Namespace": "AWS/EBS",
        "Dimensions": [
          {
            "Name": "VolumeId",
            "Value": "vol-1234567890"
          }
        ],
        "Statistic": "Maximum",
        "Period": 300,
        "EvaluationPeriods": 1,
        "Threshold": 0,
        "ComparisonOperator": "GreaterThanThreshold",
        "AlarmActions": [
          { "Ref": "MySNSTopic" }
        ]
      }
    }
  }
}
```

---

# ⭐ Best Practices for EBS

### ✔ Enable automatic snapshots using Data Lifecycle Manager

### ✔ Always use **gp3** (cheapest + predictable performance)

### ✔ Use io2 for heavy database workloads

### ✔ Monitor BurstBalance for gp2/st1/sc1

### ✔ Use separate EBS volumes for:

* OS
* Application
* Database
* Logs

---

# Want implementation examples?

I can provide:

📌 EBS → Snapshots automation
📌 EBS → Auto-recovery alarm
📌 EBS → Performance monitoring dashboard
📌 Terraform or CloudFormation templates

Just tell me **which one you want**.
