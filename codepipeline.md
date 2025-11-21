Below is a **very easy, step-by-step guide** to set up **AWS CodePipeline + CodeBuild + S3/EC2** for a **Node.js app**.
This is the exact real-world setup used in many MERN/AWS projects.

---

# ✅ **AWS CodePipeline for Node.js — Step-by-Step Guide**

## **📌 Final Architecture**

```
GitHub → CodePipeline → CodeBuild → (Build output) → Deploy to S3 or EC2
```

You can choose **S3 (static React build)** or **EC2 (Node.js backend)**.

I will explain **both**.

---

# ⭐ **STEP 1 — Create GitHub Repo**

Your Node.js project must have:

```
package.json
server.js  (or app.js)
buildspec.yml (we will create)
```

Commit and push code to GitHub.

---

# ⭐ **STEP 2 — Create buildspec.yml (important!)**

In the project root, create:

### **buildspec.yml**

```yaml
version: 0.2

phases:
  install:
    commands:
      - echo Installing dependencies...
      - npm install
  build:
    commands:
      - echo Building project...
      - npm run build || echo "No build script found."
artifacts:
  files:
    - '**/*'
```

**For backend Node only**, you can remove the build step.

---

# ⭐ **STEP 3 — Create S3 Bucket (optional if deploying to EC2)**

If this is **React frontend**:

```
Go to AWS Console → S3 → Create bucket → Enable static hosting
```

Note bucket name:
`my-react-app-prod`

If backend EC2 → skip.

---

# ⭐ **STEP 4 — Create IAM Role**

AWS → IAM → Create Role → **CodePipeline** + **CodeBuild** trust.

Attach:

* **AmazonS3FullAccess**
* **AWSCodePipelineFullAccess**
* **AWSCodeBuildAdminAccess**
* (If EC2 deploy) **AmazonEC2FullAccess**

---

# ⭐ **STEP 5 — Create CodeBuild Project**

AWS Console → **CodeBuild** → Create Build Project:

### Settings

* **Source** → GitHub → connect repo
* **Environment**:

  * Runtime → **Ubuntu / Node.js 18**
  * Privileged: **false** (unless Docker)
* **Buildspec**:

  * Choose “Use buildspec.yml from source”
* **Artifacts**:

  * If deploying to S3 → choose S3 bucket
  * If deploying to EC2 → choose “No artifacts”

---

# ⭐ **STEP 6 — Create CodePipeline**

AWS Console → CodePipeline → Create Pipeline:

### **1. Source Stage**

* Provider: **GitHub**
* Repo: your nodejs repo
* Branch: `main`

### **2. Build Stage**

* Provider: **CodeBuild**
* Select the build project you created

### **3A. Deploy Stage — S3 (React frontend)**

* Provider: **S3**
* Bucket: your hosting bucket
* Deploy: "Extract artifacts"

### **3B. Deploy Stage — EC2 (Node backend)**

Two options:

### **Option 1: Use CodeDeploy (recommended)**

Requires:

* Install CodeDeploy agent on EC2
* Add `appspec.yml` to repo

**appspec.yml example (Node.js backend):**

```yaml
version: 0.0
os: linux
files:
  - source: /
    destination: /home/ec2-user/myapp
hooks:
  AfterInstall:
    - location: scripts/restart_server.sh
      timeout: 300
      runas: ec2-user
```

**restart_server.sh**

```bash
#!/bin/bash
pm2 restart all || pm2 start server.js --name myapp
```

Make it executable:

```bash
chmod +x scripts/restart_server.sh
```

### **Option 2: Use SSM (simple)**

Pipeline → Deploy → AWS Systems Manager → Run Command → Restart PM2
(Not recommended for production, but works.)

---

# ⭐ **STEP 7 — Push Code & Trigger Pipeline**

Every push to GitHub `main` branch will now:

1. Start CodePipeline
2. Pull latest code
3. Trigger CodeBuild
4. Build Node app
5. Deploy to S3 or EC2

---

# ⭐ **If You Want Full Setup for MERN Stack**

Tell me:

✔ React frontend deploy to S3 + CloudFront?
✔ Node.js backend deploy to EC2 (PM2)?
✔ Add environment variables using SSM Parameter Store?
✔ Add HTTPS using ACM + CloudFront/ALB?

I can generate the **complete production-level AWS CI/CD setup** for your project.

