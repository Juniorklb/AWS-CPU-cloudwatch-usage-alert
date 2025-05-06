
# 📊 AWS CloudWatch CPU Usage Alert Project
![AWS](https://img.shields.io/badge/Built%20with-AWS-orange?style=flat&logo=amazonaws)
![Project Status](https://img.shields.io/badge/status-in--progress-yellow)

This project demonstrates how to monitor an Amazon EC2 instance's CPU usage and trigger an alert using Amazon CloudWatch and Amazon SNS. It's ideal for learning AWS monitoring, automation, and alerting best practices.

---

## 🚀 Project Objectives

- Monitor EC2 instance CPU utilization using Amazon CloudWatch.
- Trigger an alert when CPU usage exceeds a threshold (e.g., 80%).
- Send a notification using Amazon SNS to a subscribed email.
- (Optional) Simulate high CPU usage to test the alert.

---

## 🛠️ Prerequisites

- **Amazon EC2** – Virtual server to monitor.
- **Amazon CloudWatch** – Monitoring and alerting service.
- **Amazon SNS (Simple Notification Service)** – Sends email notifications.
- **AWS Console / AWS CLI / Terraform** – Configuration and management.

---

## 🧭 Architecture Overview




---

## 📋 Step-by-Step Implementation

### 1. Launch EC2 Instance
- Launch a new Amazon EC2 instance (Amazon Linux 2 recommended).
- Allow SSH access.
- (Optional) Enable detailed monitoring for 1-minute metrics.

### 2. Create SNS Topic
- Go to **Amazon SNS > Topics** and create a topic named `HighCPUUsageAlert`.
- Create a subscription to your email and confirm it.

### 3. Create a CloudWatch Alarm
- Go to **CloudWatch > Alarms > Create Alarm**.
- Select metric: **EC2 > Per-Instance Metrics > CPUUtilization**.
- Set conditions:
  - Threshold: `Greater than 80%`
  - Period: `5 minutes`
  - Evaluation Periods: `1`
- Set action: **Send notification to the SNS topic** created above.

### 4. Simulate High CPU Usage (Optional)
SSH into your instance and run:
     
    bash
    sudo yum install -y stress
    stress --cpu 2 --timeout 300
## Conclusion

We have successfully created a CloudWatch CPU usage alert in AWS. We learned how to configure an SNS topic for notifications, set threshold metrics, and verify alarms both through the console and the CLI. We also covered key troubleshooting tips to ensure the alert functions correctly. By following these steps, we have taken an important step toward proactive and cost-effective monitoring of our AWS infrastructure.

- Project created as part of my AWS monitoring practice portfolio.
