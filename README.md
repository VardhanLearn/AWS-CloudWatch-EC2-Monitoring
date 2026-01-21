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
===================================================================================================================================

