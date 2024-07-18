---

# Hosting a Static Website on AWS

This repository contains scripts and configurations used to deploy a static HTML web application on AWS infrastructure.

## Project Overview

The project leverages AWS services to host a static website. Below is an outline of the setup and components used:

1. **Virtual Private Cloud (VPC)**:
   - Configured a VPC spanning two availability zones with public and private subnets for enhanced security and fault tolerance.

2. **Internet Gateway**:
   - Deployed an Internet Gateway to enable connectivity between VPC instances and the internet.

3. **Security Groups**:
   - Implemented Security Groups as network firewalls to control traffic to EC2 instances.

4. **Availability Zones**:
   - Utilized two Availability Zones to ensure high availability of the system.

5. **Subnets**:
   - Public subnets used for resources like NAT Gateway and Application Load Balancer.
   - Private subnets used for web servers (EC2 instances) to enhance security.

6. **EC2 Instances**:
   - Hosted the static website on EC2 instances within the private subnets.

7. **Application Load Balancer (ALB)**:
   - Configured an ALB and target group to distribute web traffic across an Auto Scaling Group of EC2 instances in multiple Availability Zones.

8. **Auto Scaling Group**:
   - Utilized Auto Scaling Group to automatically manage EC2 instances based on traffic load, ensuring availability, fault tolerance, and scalability.

9. **Version Control**:
   - Managed web files using GitHub for version control and collaboration.

10. **SSL/TLS Security**:
    - Secured application communications using AWS Certificate Manager for SSL/TLS certificates.

11. **Monitoring and Alerts**:
    - Configured Simple Notification Service (SNS) to send alerts about activities within the Auto Scaling Group.

12. **Domain Name**:
    - Registered a domain name and set up DNS records using Amazon Route 53.

## Deployment Scripts

The following script was used to automate the deployment of the static website on an EC2 instance:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

This script installs Apache HTTP Server, retrieves the static website files from GitHub, and starts serving them.

## Diagram

For a visual representation of the architecture, please refer to the diagram provided in the repository (`architecture-diagram.png`).

## Notes

- Ensure that appropriate IAM roles, policies, and permissions are set up for secure and efficient operation.
- Regularly update and patch all components to maintain security and performance.

---

