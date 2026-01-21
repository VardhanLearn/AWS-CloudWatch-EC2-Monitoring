# AWS CloudWatch Monitoring (EC2 Metrics + Logs + Alarm + Dashboard)
A simple setup to monitor EC2 instance performance and health using AWS CloudWatch metrics, logs, and alarms.

<img width="1004" height="346" alt="Architecture Diagram" src="https://github.com/user-attachments/assets/02d236b4-db51-47ed-bce1-215f0dc54534" />

A beginner-friendly **DevOps monitoring project** using **AWS CloudWatch** to monitor an **Ubuntu EC2 instance** with:
- System Metrics (CPU, Memory, Disk)
- Log Monitoring (syslog)
- CloudWatch Alarms + SNS Email Notification
- CloudWatch Dashboard

This project is designed as a **real-time monitoring setup** and is also **interview-ready** for DevOps / Cloud Engineer roles.

---

## 📌 Project Overview

### ✅ What we Monitor
| Monitoring Type | Service | What we Track |
|---|---|---|
| Metrics | CloudWatch Metrics | CPU, Memory, Disk utilization |
| Logs | CloudWatch Logs | `/var/log/syslog` |
| Alerts | CloudWatch Alarms + SNS | Notify via Email when CPU > 70% |
| Visualization | CloudWatch Dashboard | Unified monitoring dashboard |

---

## 🛠️ Tech Stack / Tools Used
- **AWS EC2 (Ubuntu 22.04)**
- **AWS CloudWatch**
- **CloudWatch Agent**
- **AWS SNS**
- Linux Commands (`wget`, `dpkg`, `stress`)

---

## 🎯 Use Case (Real-world)
In real production environments, CloudWatch is used to:
- Monitor EC2 instance health
- Track CPU, Memory & Disk usage trends
- Centralize logs for debugging
- Trigger alerts when systems exceed thresholds
- Build dashboards for SRE/DevOps monitoring

---
✅ **Prerequisites**

Before starting, ensure you have:

AWS Requirements

🔹AWS Account |🔹IAM user permissions: 🔹EC2FullAccess |🔹CloudWatchFullAccess |🔹 SNSFullAccess |🔹IAMFullAccess |🔹Local Requirements | SSH Client .pem key pair downloaded |🔹Internet access

---

**🚀 Step-by-Step Deployment Guide**

**Step 1: Launch EC2 Instance**

🔹Launch an Ubuntu 22.04 EC2 instance: |🔹AMI: Ubuntu 22.04 |🔹Instance Type: t2.micro |🔹Enable inbound rule: 🔹SSH (22) → My IP

**Step 2: SSH into EC2**

🔹chmod 400 cloudwatch.pem

🔹ssh -i cloudwatch.pem ubuntu@<EC2_PUBLIC_IP>

---
**Step 3: Install CloudWatch Agent**

🔹sudo apt update -y

🔹sudo apt install -y unzip wget


**Download & install:**

wget https://amazoncloudwatch-agent.s3.amazonaws.com/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
sudo dpkg -i amazon-cloudwatch-agent.deb

---
**Step 4: Create IAM Role for EC2 (Important)**

🔹 Create an IAM role and attach:

🔹 CloudWatchAgentServerPolicy

🔵 **Role name**:

🔹EC2CloudWatchAgentRole

🔹Attach the role to the EC2 instance:

**EC2 → Instance → Actions → Security → Modify IAM Role**

---

**Step 5: Create CloudWatch Agent Config File**

Create the config directory:

🔹sudo mkdir -p /opt/aws/amazon-cloudwatch-agent/etc/

Create config file:

🔹sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json

---
**Step 6: Start CloudWatch Agent**

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
-a fetch-config \
-m ec2 \
-c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json \
-s

**Check status:**

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status

---
**Step 7: Verify Metrics & Logs in AWS Console**

🔹Go to:

✅ CloudWatch → Metrics

🔹Check namespace: CustomEC2Monitoring

✅ CloudWatch → Logs → Log groups

Confirm log group exists:

🔹/ec2/cloudwatch/syslog

---
**Step 8: Create CloudWatch Alarm + SNS Notification**

🔹Go to:

**CloudWatch → Alarms → Create Alarm**

🔹Select:

**Metric: EC2 → CPUUtilization**

🔹Condition: CPU > 70%

🔹Action: SNS Topic (email notification)

🔹Confirm SNS subscription from your email.

---
**Step 9: Create a CloudWatch Dashboard**

**CloudWatch → Dashboards → Create Dashboard**

Add widgets:

🔹CPUUtilization

🔹mem_used_percent

🔹Disk used percent

**🧪 Testing (Trigger Alarm)**

Install stress tool:

🔹sudo apt install -y stress

🔹Generate CPU load:

🔹stress --cpu 2 --timeout 180


**Now verify:**

🔹Alarm changes state to ALARM

🔹Email notification received

**Stop early**:

pkill stress

✅ Future Enhancements

🔹 Add Nginx/Apache access logs monitoring
🔹 Use Terraform for Infrastructure provisioning
🔹 Auto-deploy via Jenkins pipeline
🔹 Add anomaly detection alarms

---

<img width="1855" height="784" alt="InstanceRunning" src="https://github.com/user-attachments/assets/48527af3-e79a-4ddc-a994-ad733d644ace" />
<img width="1854" height="783" alt="CloudwatchAlrams" src="https://github.com/user-attachments/assets/5baf8736-13c2-4daf-a4d8-67645f2eddd3" />
<img width="1854" height="869" alt="CloudwatchLogs" src="https://github.com/user-attachments/assets/55f05ab6-a4e1-4e17-817f-44748083b504" />
<img width="1854" height="705" alt="CustomEC2Monitoring" src="https://github.com/user-attachments/assets/0ddbcbbe-0f01-4a15-8dd6-0709df0cccaa" />
<img width="1795" height="803" alt="BeforeLoad" src="https://github.com/user-attachments/assets/67cf71f4-9917-460e-a9e6-045375ccc009" />
<img width="1795" height="803" alt="AfterLoad" src="https://github.com/user-attachments/assets/de2d3db3-b92c-427d-b5db-71acbff495b8" />
<img width="348" height="681" alt="MailReceived 70" src="https://github.com/user-attachments/assets/a4ce2e7d-0ec9-46e6-97ef-bc167e5f8fa7" />


---
**👨‍💻 Author**

⭐ **Vardhan Kandregula**

⭐ **DevOps Engineer | AWS | CI/CD | Kubernetes | Monitoring**
