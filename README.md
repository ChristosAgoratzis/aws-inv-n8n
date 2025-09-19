
---

## 🚀 Workflows

### 1. Discovery
- Trigger: Scheduled (every 10–15 minutes)
- Actions:
  - Fetch AWS resources using AWS nodes / HTTP API
  - Store results in PostgreSQL or Elastic
  - Emit event `ResourceDiscovered`

### 2. Compliance
- Trigger: New resource or scheduled check
- Actions:
  - Validate **tags** (e.g. `Owner`, `Environment`)
  - Check if S3 buckets are **encrypted** and **not public**
  - Verify EC2 instances follow security group policies
- Emit event `NonCompliantResource`

### 3. Notification
- Trigger: Compliance violation
- Actions:
  - Send alert to Slack or Email
  - Include resource ID, violation type, and suggested fix

### 4. Remediation (optional)
- Trigger: Non-compliant resource
- Actions:
  - Execute AWS CLI command (e.g. stop EC2, fix tags)
  - Log action to database

---

## 🛠️ Tech Stack
- **n8n** (workflow automation, self-hosted with Docker)
- **AWS** (EC2, S3, RDS, IAM, EventBridge)
- **PostgreSQL** or **ElasticSearch** for inventory
- **Slack API** or **SMTP** for notifications
- **Docker Compose** for local deployment

---

## ▶️ Getting Started

### 1. Clone Repo & Start n8n
```bash
git clone https://github.com/<your-username>/aws-n8n-inventory.git
cd aws-n8n-inventory
docker-compose up -d
