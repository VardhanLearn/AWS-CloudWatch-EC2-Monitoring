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

**Step 3: Install CloudWatch Agent**

🔹sudo apt update -y

🔹sudo apt install -y unzip wget


**Download & install:**

wget https://amazoncloudwatch-agent.s3.amazonaws.com/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
sudo dpkg -i amazon-cloudwatch-agent.deb

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

