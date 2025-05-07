
# 📊 AWS CloudWatch CPU Usage Alert Project
![AWS](https://img.shields.io/badge/Built%20with-AWS-orange?style=flat&logo=amazonaws)
![Project Status](https://img.shields.io/badge/status-in--progress-yellow)

This project demonstrates how to monitor an Amazon EC2 instance's CPU usage and trigger an alert using Amazon CloudWatch and Amazon SNS. It's ideal for learning AWS monitoring, automation, and alerting best practices.

---

## Project Objectives

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

## 📋 Step-by-Step Implementation
  
### Step 1: Launch an EC2 Instance    
- Go to the AWS Console:
- Navigate to EC2 from the AWS Management Console.
-  Click “Launch Instance” and configure as follows:
  
  ![image alt](https://github.com/Juniorklb/AWS-CPU-cloudwatch-usage-alert/blob/48aec178d0986b93e5d9f3d242cbef4571d45aca/image/EC2.PNG)

| Setting                  | Value                           |
|--------------------------|---------------------------------|
| **Name**                 | `MonitoringTestInstance`        |
| **AMI**                  | Amazon Linux 2 or Ubuntu 20.04  |
| **Instance Type**        | `t2.micro` (Free Tier eligible) |
| **Key Pair**             | Create or choose an existing one |
| **Network Settings**     | Allow SSH (port 22)             |
| **Monitoring**           | Enable detailed monitoring (optional) |
| **Storage**              | Default 8 GiB                   |
| **Tags**                 | (Optional) Name, Project tag    |

#### Launch the instance:
- Click Launch Instance and wait until its State = running.

#### 💻 Connect to Your Instance
- Once it’s running, click Connect, and follow the SSH instructions:

 `` ssh -i your-key.pem ec2-user@your-ec2-public-ip``

## 2. Create SNS Topic
### Step 2: Create an SNS Topic (Email Notification)
- Go to the AWS Console:
- Open the SNS (Simple Notification Service) dashboard from the AWS console.

- Create a Topic:
- Click “Topics” > “Create topic”

- Choose Standard as the type.

- Set the following:

    - Name: HighCPUUsageAlert

    - (Optional) Display name: CPUAlert
- Click Create topic
  
![image alt](https://github.com/Juniorklb/AWS-CPU-cloudwatch-usage-alert/blob/2434d33a3e419f0b7351dbf50a13f347366a4704/image/SNNS.PNG)

### Create an Email Subscription:
- Inside your new topic ``(HighCPUUsageAlert)``, click “Create subscription”
- Set:
   - Protocol: ``Email``
   - Endpoint: Your email address (where you want to receive alerts)
- Click Create subscription

## 📩 Confirm Your Subscription:

- Go to your inbox and confirm the SNS subscription by clicking the link in the confirmation email titled:

    `` "AWS Notification - Subscription Confirmation"``

- ⚠️ You must confirm this email for the alerts to work!
  
 ![image alt  width="400" ](https://github.com/Juniorklb/AWS-CPU-cloudwatch-usage-alert/blob/a6d533a9c1a667080f5f3568a4aa1b9326c3f831/image/IMG_6838.jpeg) 
 
### Step 3: Create a CloudWatch Alarm for High CPU Usage
#### Go to the AWS Console:
- Navigate to CloudWatch > Alarms.

- Create an Alarm:
- Click “Create Alarm”
- Click “Select Metric”
- Click “Select Metric”
#### Choose Metric:
- In the metric browser, choose:

    - Browse > EC2 > Per-Instance Metrics > CPUUtilization

- Select the checkbox next to your EC2 instance’s CPUUtilization

#### Configure Metric:
  
- Set the following:
  
| Field                   | Value               |
|-------------------------|---------------------|
| **Period**              | `5 minutes`         |
| **Statistic**           | `Average`           |
| **Threshold type**      | `Static`            |
| **Condition**           | `Greater than 80`   |
| **Datapoints to alarm** | `1 out of 1` (or 2/3 for more stability) |

- Click Next.  
#### Configure Actions:
- Under Alarm state trigger, select:

   - In alarm

- Choose Send a notification to an SNS topic

- Select your topic:``HighCPUUsageAlert``

- Click Next.
  
 ####  Add Alarm Name and Description:
- Alarm name: ``HighCPUUsageAlarm``

- Description (optional): Alert when CPU exceeds 80% for 5 minutes

- Click Next, then Create Alarm.
 ![image alt](https://github.com/Juniorklb/AWS-CPU-cloudwatch-usage-alert/blob/631d03d5662e6e3c5efc003791fa4d8be14a34c0/image/metriccc.PNG)

### Step 4: Simulate High CPU Usage on EC2
- Step 1: SSH into your EC2 Instance
- Use your terminal:
 `` ssh -i your-key.pem ec2-user@<your-ec2-public-ip>``
- For Ubuntu instances, use ``ubuntu@`` instead of ``ec2-user@.``
- Step 2: Install stress tool
- For Amazon Linux 2:
`` sudo yum install -y stress``
- For Ubuntu:
``sudo apt update``
``sudo apt install -y stress``
- Step 3: Run the Stress Test
 `` stress --cpu 2 --timeout 300``
- This will max out 2 CPU cores for 5 minutes.
  
##  Step 4: Monitor Alarm in CloudWatch

- Go to CloudWatch > Alarms

- Watch the ``HighCPUUsageAlarm``

- Within 5–10 minutes, the status should change from OK → ALARM

##  Step 5: Check Your Email

- You should receive an email alert from SNS when the alarm triggers.



## Conclusion

We have successfully created a CloudWatch CPU usage alert in AWS. We learned how to configure an SNS topic for notifications, set threshold metrics, and verify alarms both through the console and the CLI. We also covered key troubleshooting tips to ensure the alert functions correctly. By following these steps, we have taken an important step toward proactive and cost-effective monitoring of our AWS infrastructure.

- Project created as part of my AWS monitoring practice portfolio.
