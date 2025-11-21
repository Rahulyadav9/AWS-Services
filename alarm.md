---

# ✅ **What is an AWS CloudWatch Alarm?**

An **AWS CloudWatch Alarm** monitors a metric (CPU, memory, errors, latency, etc.) and **triggers an action** when the value crosses a defined threshold.

### **Common Actions:**

* Send an SNS notification (email/SMS)
* Trigger an Auto Scaling policy
* Restart an EC2 instance
* Stop/Terminate an EC2 instance
* Execute a Lambda function

---

# 🎯 **Common Use Cases**

| Use Case           | Example Metric                       |
| ------------------ | ------------------------------------ |
| EC2 high CPU       | `CPUUtilization > 80% for 5 minutes` |
| API Gateway errors | `5XXError count > 10`                |
| Lambda throttles   | `Throttles > 0`                      |
| S3 request metrics | `4xxErrors`                          |
| DynamoDB           | `ReadThrottleEvents`                 |

---

# ⚙️ **How CloudWatch Alarm Works**

1. CloudWatch receives metrics every **1 minute or 5 minutes**.
2. Alarm compares metric with your **threshold**.
3. When condition meets, alarm goes to:

   * **ALARM** state → triggers actions
4. When back to normal → **OK** state
5. If metric stops coming → **INSUFFICIENT_DATA**

---

# 🧭 **How to Create a CloudWatch Alarm (Step-by-Step)**

### **STEP 1 — Open CloudWatch**

Go to:
**AWS Console → CloudWatch → Alarms → Create Alarm**

---

### **STEP 2 — Select Metric**

Choose:

* EC2 → Per-Instance Metrics → CPUUtilization
  or
* Lambda → Errors / Duration
  or
* API Gateway → 5XXError

Select your metric.

---

### **STEP 3 — Set Threshold**

Example for high CPU:

```
Alarm when CPUUtilization > 80%
For 5 data points of 1 minute each
```

Settings:

* **Threshold type:** Static
* **Condition:** Greater than
* **Value:** 80

---

### **STEP 4 — Configure Actions**

Choose how AWS should inform you:

* **Add SNS topic**
  Example: send email at `"dev-team@company.com"`

or choose:

* **AutoScaling action**
* **EC2 Action** (stop, reboot, terminate)
* **Lambda Action**

---

### **STEP 5 — Name the Alarm**

Example:

```
High-CPU-Alarm-EC2-Instance123
```

---

### **STEP 6 — Create Alarm**

Done 🎉

---

# 📡 Example AWS CloudWatch Alarm (Terraform or JSON)

### **CloudFormation JSON**

```json
{
  "Resources": {
    "HighCPUAlarm": {
      "Type": "AWS::CloudWatch::Alarm",
      "Properties": {
        "AlarmName": "HighCPUAlarm",
        "MetricName": "CPUUtilization",
        "Namespace": "AWS/EC2",
        "Statistic": "Average",
        "Period": 60,
        "EvaluationPeriods": 5,
        "Threshold": 80,
        "ComparisonOperator": "GreaterThanThreshold",
        "AlarmActions": [
          {"Ref": "MySNSTopic"}
        ]
      }
    }
  }
}
```

---

# 🔍 Types of CloudWatch Alarms

### **1. Metric Alarm**

* Based on EC2, Lambda, API, DynamoDB metrics

### **2. Composite Alarm**

* Combine multiple alarms using AND/OR logic
* Example → Alarm only if CPU > 80 AND Memory > 80

### **3. Anomaly Detection Alarm**

* Uses ML to detect unusual patterns
  Example: if latency is suddenly abnormal.

---

# 🛠 AWS Alarms Best Practices

### ✔ **Set CPU/Memory alarms for EC2**

```
CPU > 80%
Memory > 85%
Disk space < 20%
```

### ✔ **Set error alarms for APIs**

```
5XXErrors > 5
Latency > 1s
```

### ✔ **Set throttling alarms for Lambda/DynamoDB**

```
Throttles > 0
```

### ✔ **Always send notification to SNS**

So you get alerts immediately.

---

# Want me to create?

✅ CloudWatch Alarm
✅ SNS setup
✅ EC2 AutoRecovery
✅ Terraform/CloudFormation alarm template
Just tell me what service you want to monitor.
