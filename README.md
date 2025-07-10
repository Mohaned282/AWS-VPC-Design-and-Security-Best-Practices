AWS VPC Design & Security Best Practices (AWS Console Deployment):
This project outlines the manual setup of a secure and scalable AWS Virtual Private Cloud (VPC) using the AWS Management Console. The configuration includes public and private subnets, security controls (Security Groups and Network ACLs), IAM roles and logging with AWS CloudTrail and all aligned with AWS best practices.

Overview:
Designing a well-architected network is crucial for any cloud infrastructure. This guide walks through the manual configuration of a production-ready and secure VPC environment using the AWS Console without automation.
 
Key Components:
•VPC: Custom VPC with IPv4 CIDR block (10.0.0.0/16)
•Public Subnets: For internet-facing resources (Web servers)
•Private Subnets: For backend/internal resources (Database Servers)
•Internet Gateway (IGW): To allow internet access for public subnets
•NAT Gateway: Enables private subnets to access the internet securely
•Route Tables: Separate route tables for public and private subnets
•Security Groups: Restrict traffic to and from EC2 instances
•NACLs: Provide an extra layer of subnet-level security
•IAM Roles & Policies: For secure resource access and permissions
•AWS CloudTrail: To monitor and log API calls and user activity

Objectives:
•Design a secure and isolated VPC environment using the AWS Console
•Apply best security practices using IAM, NACLs and Security Groups
•Enable full auditing and monitoring with AWS CloudTrail

Features:
•Security: Layered security with Security Groups and NACLs
•Auditability: Full tracking of user and API activity via CloudTrail
•Scalability: Modular network design for future expansion
•Compliance: Designed with best practices for secure infrastructure

Deployment Steps (AWS Console):
1.Create a VPC
•Navigate to VPC > Your VPCs > "Create VPC"
•Use CIDR block: 10.0.0.0/16
•Choose "VPC only" option

2.Create Subnets:
•Create at least two Public Subnets in different AZs (10.0.1.0/24, 10.0.3.0/24)
•Create at least two Private Subnets in different AZs (10.0.2.0/24, 10.0.4.0/24)

3.Create and Attach an Internet Gateway:
•Go to Internet Gateways > Create IGW > Attach to your VPC

4. Create Route Tables:
•Create Public Route Table:
Add route: 0.0.0.0/0 > IGW
Associate with public subnets
•Create Private Route Table:
Will be used for private subnets with NAT Gateway

5.Create a NAT Gateway:
•Go to NAT Gateways
•Allocate an Elastic IP and assign it to the NAT Gateway in a public subnet
•Add route in Private Route Table: 0.0.0.0/0 > NAT Gateway

6.Configure Security Groups:
•Create Web Servers Security Group (allow HTTPS from 0.0.0.0/0)
•Create Database Servers Security Group (allow traffic only from Web SG)

7.Configure NACLs (It's optional for extra subnet-level security):
•Allow required inbound/outbound rules for both public and private subnets

8.Set Up IAM Roles & Policies:
•Create IAM roles with least privilege for EC2 and CloudTrail and future services

9.Enable CloudTrail:
•Go to CloudTrail > Trails
•Create trail > Enable logging for all regions > Store logs in an S3 bucket

Results and Benefits:
Aspect	Impact
Security	Enforced via multi-layered controls (SGs, NACLs, IAM)
Auditability	CloudTrail records API activity across AWS
Availability	Public/private subnet structure supports high-availability designs
Scalability	Modular VPC design allows easy future growth

Lessons Learned:
•Hands-on VPC configuration helps understand core AWS networking principles
•Security configurations must be tightly managed to avoid exposure
•CloudTrail is essential for any production AWS account

Author:
Mohaned Mohamed
AWS Network Engineer | AWS Solutions Architect Associate | CCNP Security | PCNSE7 | VPC | Transit Gateway | BGP | VPN | Cloud Security | Linux | CloudFormation
