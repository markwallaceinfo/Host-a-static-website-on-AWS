# Hosting a Static Website on AWS

## Overview
This project details the steps involved in hosting a static HTML web application on AWS using various services and resources provided by the platform. The deployment utilizes a combination of EC2 instances, Virtual Private Cloud (VPC), Internet Gateway, Security Groups, Route 53, and other AWS services to ensure reliability, scalability, and security of the hosted website.

## Project Components and Configuration
1. **Virtual Private Cloud (VPC):**
   - Configured with both public and private subnets across two different availability zones for high availability.
2. **Internet Gateway:**
   - Deployed to facilitate connectivity between VPC instances and the wider Internet.
3. **Security Groups:**
   - Implemented as a network firewall mechanism to control traffic to and from EC2 instances.
4. **Availability Zones:**
   - Leveraged for enhanced system reliability and fault tolerance.
5. **EC2 Instances:**
   - Web servers positioned within Private Subnets for enhanced security.
   - Hosted the website on EC2 Instances.
   - Utilized EC2 Instance Connect Endpoint for secure connections.
6. **NAT Gateway:**
   - Enabled instances in private subnets to access the Internet.
7. **Application Load Balancer (ALB):**
   - Employed for evenly distributing web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
8. **Auto Scaling Group:**
   - Automatically managed EC2 instances to ensure website availability, scalability, fault tolerance, and elasticity.
9. **GitHub:**
   - Web files stored for version control and collaboration.
10. **Certificate Manager:**
    - Used to secure application communications.
11. **Simple Notification Service (SNS):**
    - Configured to alert about activities within the Auto Scaling Group.
12. **Route 53:**
    - Registered the domain name and set up DNS records.

## Deployment Script
The provided Bash script automates the deployment process of the static website on an AWS EC2 instance. It performs the following tasks:
- Updates installed packages.
- Installs Apache HTTP Server.
- Clones the project GitHub repository.
- Copies files to the Apache web root.
- Enables and starts the Apache HTTP Server.

### Usage
1. Ensure that you have necessary permissions to execute the script.
2. Run the script on an AWS EC2 instance.
3. Access the website using the instance's public IP or domain name.

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

## License
This project is licensed under the [MIT License](LICENSE).

---

