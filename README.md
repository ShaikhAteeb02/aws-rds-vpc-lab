# EC2-based Web Server with S3 Backup

Deploy a robust and secure Apache web server on AWS EC2 and automate website file backups to Amazon S3. This project guides you through infrastructure setup, permissions, and CLI configuration to build a scalable, reliable solution for hosting and safeguarding your web content.

---

## Features

- Launch Ubuntu 24.04 EC2 instance with secure SSH and HTTP access
- Install and configure Apache web server
- Create and configure an S3 bucket with secure settings
- Create and attach IAM role with S3 full access to EC2
- Install AWS CLI and verify credentials via IAM role
- Automate backup of files from EC2 to S3 using AWS CLI commands

---

## Architecture Overview

- **EC2 Instance**: Ubuntu VM runs Apache web server
- **Apache2**: Serves the website content on port 80
- **S3 Bucket**: Stores backup files securely with encryption and no public access
- **IAM Role**: Grants EC2 instance permissions to manage S3
- **AWS CLI**: Performs backup uploads and file management from EC2

---

## Setup Instructions

1. **Create an S3 Bucket**
    - Use AWS Console to create a bucket (e.g., `my-bucket-ateeb-01`)
    - Keep public access blocked and enable SSE-S3 encryption

2. **Launch EC2 Instance**
    - Select Ubuntu Server 24.04 LTS AMI, choose t3.micro instance
    - Configure security group for SSH (restricted to your IP) and HTTP (open)
    - Enable auto-assign public IP

3. **Create and Attach IAM Role**
    - Create IAM role with AmazonS3FullAccess permission
    - Attach this role to the EC2 instance for automated access rights

4. **Install Apache on EC2**
    - SSH into EC2 instance
    - Update packages and install Apache:  
      `sudo apt update -y`  
      `sudo apt install apache2 -y`  
    - Enable and start Apache:  
      `sudo systemctl enable apache2`  
      `sudo systemctl start apache2`

5. **Install AWS CLI**
    - Install the AWS CLI via snap:  
      `sudo snap install aws-cli --classic`  
    - Verify access with IAM role:  
      `aws sts get-caller-identity`  

6. **Backup Files to S3**
    - Create a file on EC2:  
      `echo "Hello from EC2 on $(date)" > /home/ubuntu/example-file.txt`  
    - Upload file to S3 bucket:  
      `aws s3 cp /home/ubuntu/example-file.txt s3://my-bucket-ateeb-01/example-file.txt`

---

## Usage

```
# Connect
ssh -i "keypair_2.pem" ubuntu@<EC2_PUBLIC_IP>

# Test Apache
curl http://<EC2_PUBLIC_IP>

# Backup file upload example
aws s3 cp /path/to/file s3://<YOUR_BUCKET_NAME>/filename
```

---

## Connect with Me

[![GitHub](https://img.shields.io/badge/GitHub-ShaikhAteeb02-181717?style=for-the-badge&logo=github)](https://github.com/ShaikhAteeb02)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-AteebAhmed%20Shaikh-0A66C2?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/ateeb-ahmed-shaikh-932234192/)

---
