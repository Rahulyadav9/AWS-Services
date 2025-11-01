| Service          | Description            |
| ---------------- | ---------------------- |
| **CodeCommit**   | Git repositories       |
| **CodeBuild**    | Build & test code      |
| **CodeDeploy**   | Automate deployments   |
| **CodePipeline** | CI/CD pipeline service |


Here’s a **complete AWS CodePipeline interview Q&A guide** — from **basic to advanced concepts**, including **real-world scenarios** often asked in DevOps or cloud engineering interviews 👇

---

## 🧩 **Basic CodePipeline Interview Questions**

### **1. What is AWS CodePipeline?**

**AWS CodePipeline** is a **continuous integration and continuous delivery (CI/CD) service** that automates the build, test, and deployment phases of your release process every time code changes.

It helps you deliver software **quickly and reliably**.

---

### **2. What are the main components (stages) of CodePipeline?**

1. **Source** – Retrieves code from source control (e.g., GitHub, CodeCommit, S3).
2. **Build** – Compiles and packages the source code (e.g., CodeBuild, Jenkins).
3. **Test** – Runs automated tests.
4. **Deploy** – Deploys to services (e.g., CodeDeploy, ECS, Lambda, S3).
5. **Approval** (optional) – Manual approval before proceeding to next stage.

---

### **3. What is the purpose of AWS CodePipeline?**

To **automate the release process**, ensuring:

* Faster delivery
* Fewer manual steps
* Consistent deployments
* Integration with AWS and third-party tools

---

### **4. What is a pipeline execution?**

A **pipeline execution** is a single run of the entire CI/CD process triggered by a **code change**, **manual execution**, or a **schedule**.

---

### **5. What are common AWS services integrated with CodePipeline?**

* **CodeCommit / GitHub / Bitbucket** (source)
* **CodeBuild / Jenkins** (build)
* **CodeDeploy / ECS / Lambda / S3** (deploy)
* **CloudWatch Events / SNS** (notifications)
* **CloudFormation / Terraform** (infrastructure deployment)

---

## ⚙️ **Intermediate CodePipeline Interview Questions**

### **6. What is the difference between CodePipeline and CodeBuild?**

| Feature | CodePipeline                | CodeBuild                        |
| ------- | --------------------------- | -------------------------------- |
| Purpose | Orchestration (workflow)    | Build/Compile source code        |
| Type    | CI/CD orchestration service | Build service                    |
| Input   | Code repositories           | Source code or artifacts         |
| Output  | Managed workflow execution  | Build artifact (zip, jar, image) |

---

### **7. How do you trigger a pipeline automatically?**

You can trigger CodePipeline when:

* A **commit** is made in the source repository (GitHub/CodeCommit).
* A **CloudWatch Event rule** runs on schedule.
* A **manual release** is started from the console or CLI.

---

### **8. What is an artifact in CodePipeline?**

An **artifact** is an output from one stage (e.g., build artifact) and input to another (e.g., deploy stage).
Artifacts are usually stored in **Amazon S3**.

---

### **9. How can you add manual approvals in a pipeline?**

Use a **Manual Approval action** between stages to require human approval before proceeding.
You can integrate **SNS notifications** to alert approvers.

---

### **10. What is a pipeline stage action?**

Each **stage** in CodePipeline contains **actions** — individual tasks like build, deploy, or test.
Example:

* Source Action (GitHub)
* Build Action (CodeBuild)
* Deploy Action (CodeDeploy)

---

### **11. How can you deploy an application using CodePipeline?**

Typical pipeline structure:

1. **Source** – Pull from CodeCommit
2. **Build** – Use CodeBuild to compile
3. **Deploy** – Use CodeDeploy to EC2, ECS, or Lambda

---

### **12. What are action types in CodePipeline?**

* **Source**
* **Build**
* **Test**
* **Deploy**
* **Approval**
* **Invoke** (Lambda or custom integration)

---

### **13. Can you integrate third-party tools with CodePipeline?**

✅ Yes. CodePipeline supports integrations with tools like:

* **Jenkins**
* **GitHub**
* **Bitbucket**
* **SonarQube**
* **Slack (via SNS + Lambda)**

---

### **14. What is the difference between AWS CodePipeline and Jenkins?**

| Feature    | CodePipeline               | Jenkins                         |
| ---------- | -------------------------- | ------------------------------- |
| Managed by | AWS                        | Self-hosted                     |
| Setup      | Minimal                    | Manual setup required           |
| Cost       | Pay per pipeline execution | Free (but requires infra)       |
| Plugins    | Limited (AWS services)     | Vast plugin ecosystem           |
| Use Case   | AWS-native CI/CD           | Flexible custom CI/CD pipelines |

---

### **15. What is CodePipeline YAML definition file?**

You can define your entire pipeline in **code** (YAML/JSON) — known as **pipeline-as-code**.
This allows **version control** and **automation** using CloudFormation or AWS CDK.

---

## 🔒 **Advanced CodePipeline Interview Questions**

### **16. What is cross-account deployment in CodePipeline?**

It’s when you use **one AWS account** to build and store artifacts, but **deploy** them in another AWS account (for example, Dev → Prod).
Achieved using:

* **Cross-account IAM roles**
* **Artifact bucket policies**

---

### **17. What happens if a stage in CodePipeline fails?**

* The pipeline **stops** at that stage.
* An **event** is sent to **CloudWatch / SNS** for notification.
* You can **retry** manually or fix the issue and **release** again.

---

### **18. How do you handle environment-specific deployments (Dev, QA, Prod)?**

Use **multiple pipelines** or **multiple stages** within one pipeline with:

* Different **deployment targets**
* Different **configuration files (env.json)**
* **Manual approval** before Prod stage

---

### **19. How do you secure a CodePipeline?**

* Use **IAM roles** for least privilege.
* Use **KMS encryption** for artifacts.
* Limit **S3 bucket access** (artifact storage).
* Restrict **manual approval** permissions.

---

### **20. Can you pause or retry a pipeline?**

✅ Yes.

* **Pause** using the console or CLI.
* **Retry** failed executions from a specific stage.

---

### **21. How can you integrate Lambda with CodePipeline?**

You can use **Lambda Invoke actions** to:

* Run tests
* Notify users
* Trigger downstream systems
* Validate deployment success

---

### **22. What are some CodePipeline limitations?**

* Max **50 pipelines** per region (can request increase)
* Max **20 stages** per pipeline
* No direct **branch-based pipelines** (needs separate pipelines)
* Limited **parallelism** per stage

---

### **23. What are common failure reasons in CodePipeline?**

* IAM permission issues
* Wrong S3 bucket policy
* Missing artifacts
* Buildspec.yml errors
* Failed deployment hooks in CodeDeploy

---

### **24. What is the difference between CodePipeline and CodeDeploy?**

| Feature       | CodePipeline               | CodeDeploy                |
| ------------- | -------------------------- | ------------------------- |
| Purpose       | CI/CD orchestration        | Deployment automation     |
| Deploy Target | ECS, Lambda, EC2           | EC2, Lambda, ECS          |
| Flow          | Multi-step workflow        | Deployment only           |
| Integration   | With CodeBuild, CodeCommit | Triggered by CodePipeline |

---

### **25. How can you monitor CodePipeline?**

* **CloudWatch Metrics** – Track success/failure.
* **CloudTrail Logs** – Track API calls.
* **SNS Notifications** – For alerts on stage success/failure.
* **AWS Console** – Execution history and details.

---

## 🧠 **Scenario-Based Questions**

### **26. You need to deploy your app to EC2 after every GitHub commit. How do you do it?**

1. Source: GitHub repository
2. Build: AWS CodeBuild (uses `buildspec.yml`)
3. Deploy: AWS CodeDeploy (to EC2)
4. Automate with CodePipeline

---

### **27. You want approval before production deployment — how?**

Add a **Manual Approval action** between QA and Prod stages.
Use **SNS** to notify approvers and **CloudWatch** for tracking.

---

### **28. Your build succeeds but deployment fails — how do you debug?**

* Check **CodeDeploy logs** in `/var/log/codedeploy-agent/`
* Verify **AppSpec.yml**
* Ensure **IAM roles** have deployment permissions
* Review **pipeline execution history**

---

### **29. How can you deploy infrastructure using CodePipeline?**

Use **AWS CloudFormation** or **Terraform** as a stage action for **Infrastructure as Code (IaC)**.

---

### **30. How to promote an artifact from Dev → QA → Prod environments?**

Use a **shared S3 artifact bucket**, and configure CodePipeline in each environment to pick the same artifact after approval.

---

## 🚀 **Bonus: Common Tools Used with CodePipeline**

| Stage         | Tool                     |
| ------------- | ------------------------ |
| Source        | GitHub, CodeCommit       |
| Build         | CodeBuild, Jenkins       |
| Test          | Selenium, JUnit, Postman |
| Deploy        | CodeDeploy, ECS, Lambda  |
| Notifications | SNS, Slack (via Lambda)  |

---

Would you like me to create a **PDF cheat sheet** (with CodePipeline architecture diagram and YAML example)?
It’ll include:

* Example pipeline YAML
* CI/CD flow diagram
* Key AWS service integrations
  Perfect for **last-minute interview prep or certification** revision.
