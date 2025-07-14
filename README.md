# 🚀 Scalable EC2 Web Application on AWS with ALB, ASG, CloudWatch, and SNS

This project demonstrates how to deploy a secure, highly available, and auto-scaled web application on AWS using **EC2**, **Application Load Balancer (ALB)**, and **Auto Scaling Groups (ASG)**. It integrates **CloudWatch** for performance monitoring, **SNS** for alert notifications, and **IAM roles and users** for secure access and automation.

---

## 🧱 Architecture Overview
The solution is designed for high availability, scalability, and monitoring. Here's how the components interact:

- **Users** access the application via an **Application Load Balancer (ALB)** over the internet.
- The ALB routes traffic to EC2 instances inside **private subnets** in **two Availability Zones**, managed by an **Auto Scaling Group (ASG)**.
- The EC2 instances run a PHP-based web app from a custom **AMI**, created from a pre-configured EC2 instance.
- **CloudWatch** monitors the CPU utilization of the ASG. When usage exceeds 50%, it triggers a scale-out event.
- A **CloudWatch Alarm** is linked to an **SNS Topic**, which sends email alerts on performance spikes.
- **IAM Roles** are attached to EC2 instances to allow CloudWatch metrics publishing.
- **IAM Users** are created for secure manual management via the AWS Console or CLI.

![Architecture Diagram](./SolutionArchProject.drawio.svg)

---

## 🎯 Key Features

- ✅ High availability using multi-AZ deployment
- ✅ Elastic scalability with CPU-based Auto Scaling policies
- ✅ Secure access via IAM roles (for EC2) and users (for management)
- ✅ Real-time monitoring with CloudWatch
- ✅ Email alerts on performance spikes via SNS
- ✅ Infrastructure follows AWS best practices for security and cost-efficiency

---

## ⚙️ Technologies & Services Used

- **Amazon EC2** – Web server instances
- **Amazon Machine Image (AMI)** – Custom image for ASG
- **Auto Scaling Group (ASG)** – Launches instances automatically based on demand
- **Application Load Balancer (ALB)** – Distributes traffic across instances
- **CloudWatch** – Monitors CPU usage and triggers alarms
- **SNS (Simple Notification Service)** – Sends email alerts for CloudWatch alarms
- **IAM** – Roles for EC2 access and user permissions
- **Security Groups** – Controls inbound/outbound network access

---

## 🚧 Deployment Summary

1. **Created and configured a base EC2 instance**
   - Installed Apache and a PHP app via UserData script
   - Validated application via HTTP

2. **Built a custom AMI** from the configured instance

3. **Set up an Application Load Balancer**
   - Created a target group with health checks on `/index.php`
   - Deployed ALB across 2 public subnets in different AZs

4. **Created a Launch Template**
   - Referenced the custom AMI and HTTP-access security group

5. **Created an Auto Scaling Group**
   - Used private subnets in 2 AZs
   - Attached to the ALB target group
   - Configured desired, min, and max capacities
   - Set a target-tracking policy for 50% CPU utilization

6. **Enabled Monitoring & Notifications**
   - Created a CloudWatch alarm for high CPU usage
   - Connected the alarm to an SNS topic
   - Subscribed to the topic via email for real-time alerts

7. **Secured the Infrastructure**
   - Created an IAM Role with `CloudWatchAgentServerPolicy` and attached it to EC2
   - Created an IAM User with limited access for managing the environment

---

## 🧪 Testing the Setup

- Visited the ALB DNS endpoint to access the app
- Triggered high CPU usage using the provided stress button
- Verified Auto Scaling launched new EC2 instances
- Confirmed CloudWatch alarm triggered and SNS email was received

---
## 📌 Future Enhancements

- Add SSL/TLS with ACM
- Integrate RDS and ElastiCache for persistence and caching
- Automate the entire setup using Terraform or CloudFormation
- Deploy via CI/CD using AWS CodePipeline

---

## 📌 Project Status

✅ Completed and tested successfully  
📬 Alerts received  
📈 Auto Scaling validated

---

## 🧠 Learning Outcomes

- Real-world application of EC2 Auto Scaling and ALB
- Infrastructure monitoring with CloudWatch and SNS
- Best practices for secure and scalable AWS architecture

---
