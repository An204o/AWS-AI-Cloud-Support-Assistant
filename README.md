# AWS EC2 Health Monitor & Email Alert

## Overview

The **AWS EC2 Health Monitor & Email Alert** project demonstrates how to monitor the health of an Amazon EC2 instance using AWS monitoring services. The solution automatically detects high CPU utilization and sends an email notification to administrators using Amazon SNS.

This project simulates a common cloud operations scenario where infrastructure should be monitored continuously without requiring manual intervention.

---

## Objectives

* Launch and configure an Amazon EC2 instance.
* Host a simple web application using Apache.
* Monitor CPU utilization with Amazon CloudWatch.
* Automatically notify administrators using Amazon SNS when CPU usage exceeds a defined threshold.
* Gain hands-on experience with AWS infrastructure monitoring and alerting.

---

## AWS Services Used

| Service           | Purpose                                             |
| ----------------- | --------------------------------------------------- |
| Amazon EC2        | Hosts the Linux web server                          |
| Amazon CloudWatch | Collects metrics and monitors CPU utilization       |
| Amazon SNS        | Sends email notifications when alarms are triggered |
| IAM               | Provides secure permissions for AWS services        |
| Security Groups   | Controls inbound network traffic                    |
| Amazon Linux 2023 | Operating system running on the EC2 instance        |

---

## Architecture

```
                    User
                      │
                      ▼
              Amazon EC2 Instance
                      │
                      ▼
          Amazon CloudWatch Metrics
                      │
                      ▼
            CloudWatch Alarm
                      │
                      ▼
              Amazon SNS Topic
                      │
                      ▼
              Email Notification
```

---

## Project Workflow

1. Launch an EC2 instance running Amazon Linux 2023.
2. Install and configure the Apache web server.
3. Deploy a simple HTML webpage.
4. Create a CloudWatch Alarm that monitors CPU utilization.
5. Configure an Amazon SNS topic with an email subscription.
6. Connect the CloudWatch Alarm to the SNS topic.
7. Generate CPU load on the EC2 instance.
8. Verify that CloudWatch changes the alarm state.
9. Receive an email notification from Amazon SNS.

---

## Project Structure

```
aws-ec2-health-monitor/
│
├── README.md
├── architecture/
│   └── architecture-diagram.png
│
├── screenshots/
│   ├── ec2-running.png
│   ├── website.png
│   ├── cloudwatch-alarm.png
│   ├── sns-topic.png
│   ├── email-alert.png
│   └── cpu-graph.png
│
├── scripts/
│   └── install_apache.sh
│
└── docs/
    └── deployment-guide.md
```

---

## Deployment Steps

### 1. Launch an EC2 Instance

* Amazon Linux 2023
* t2.micro or t3.micro
* Configure Security Group

  * SSH (22)
  * HTTP (80)

### 2. Connect Using SSH

```bash
ssh -i your-key.pem ec2-user@YOUR_PUBLIC_IP
```

### 3. Update the Server

```bash
sudo dnf update -y
```

### 4. Install Apache

```bash
sudo dnf install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

### 5. Create the Web Page

```bash
echo "<h1>AWS Cloud Health Monitor</h1><p>Server is running successfully.</p>" | sudo tee /var/www/html/index.html
```

### 6. Create a CloudWatch Alarm

Metric:

* CPUUtilization

Threshold:

* Greater than 70%

Evaluation Period:

* 5 minutes

### 7. Configure Amazon SNS

* Create a topic
* Subscribe your email address
* Confirm the subscription
* Attach the CloudWatch Alarm to the SNS topic

### 8. Test the Alarm

Install the stress utility.

```bash
sudo dnf install stress -y
```

Generate CPU load.

```bash
stress --cpu 4 --timeout 300
```

CloudWatch should detect the increase in CPU usage and trigger the alarm.

---

## Expected Results

* EC2 instance is running successfully.
* Apache web server is accessible from a browser.
* CloudWatch monitors CPU utilization.
* CPU usage exceeding the configured threshold triggers an alarm.
* Amazon SNS sends an email notification.
* CloudWatch returns to the **OK** state after CPU usage decreases.

---

## Skills Demonstrated

* Amazon EC2
* Linux administration
* Apache web server configuration
* CloudWatch monitoring
* CloudWatch Alarms
* Amazon SNS
* IAM fundamentals
* AWS networking
* Infrastructure monitoring
* Cloud operations
* Basic troubleshooting

---

## Screenshots

Add screenshots after completing the project.

* EC2 instance running
* Apache web page
* CloudWatch alarm
* CloudWatch metrics graph
* SNS topic
* SNS email notification
* Security Group configuration

---

## Future Improvements

Potential enhancements include:

* Monitor memory and disk utilization using the CloudWatch Agent.
* Store monitoring logs in Amazon S3.
* Use AWS Lambda to automatically restart unhealthy instances.
* Build a CloudWatch Dashboard for centralized monitoring.
* Provision the infrastructure using Terraform or AWS CloudFormation.
* Add automated deployment with GitHub Actions.

---

## Lessons Learned

Through this project I learned how AWS monitoring services work together to automate infrastructure management. I gained experience deploying Linux servers, configuring CloudWatch metrics and alarms, integrating Amazon SNS for notifications, and validating monitoring by generating CPU load on an EC2 instance. This project also reinforced the importance of proactive monitoring and automation in maintaining reliable cloud infrastructure.
