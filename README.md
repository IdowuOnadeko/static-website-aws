
---

# Static Website Hosting on AWS

This project demonstrates the deployment of a static HTML web application on AWS using a highly available, secure, and scalable architecture. The deployment utilizes various AWS services, ensuring reliability, fault tolerance, and security.

## Project Overview

The static website is hosted on EC2 instances within a Virtual Private Cloud (VPC), leveraging the following AWS resources and services:

1. **Virtual Private Cloud (VPC):** Configured with both public and private subnets across two different availability zones to enhance system reliability and fault tolerance.
   
2. **Internet Gateway:** Facilitates connectivity between the VPC instances and the wider internet.

3. **Security Groups:** Established as a network firewall mechanism to control traffic to and from the instances.

4. **Public Subnets:** Used for infrastructure components such as the NAT Gateway and Application Load Balancer (ALB).

5. **EC2 Instance Connect Endpoint:** Allows secure connections to assets within both public and private subnets.

6. **Private Subnets:** Host web servers (EC2 instances) for enhanced security.

7. **NAT Gateway:** Enables instances in private subnets to access the internet.

8. **EC2 Instances:** Host the static website.

9. **Application Load Balancer (ALB):** Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple availability zones.

10. **Auto Scaling Group:** Automatically manages the number of EC2 instances to ensure availability, scalability, fault tolerance, and elasticity.

11. **Certificate Manager:** Secures application communications by providing SSL/TLS certificates.

12. **Simple Notification Service (SNS):** Configured to send alerts about activities within the Auto Scaling Group.

13. **Route 53:** Registered the domain name and set up DNS records for the website.

## Deployment Instructions

### Prerequisites

- An AWS account with necessary permissions to create and manage the required resources.
- A registered domain name (managed through Route 53).
- Access to the GitHub repository containing the web files.

### Step-by-Step Deployment

1. **Clone the Repository:**

   ```bash
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

2. **Infrastructure Deployment:**

   - Configure the VPC with public and private subnets across two availability zones.
   - Deploy the Internet Gateway, Security Groups, and EC2 Instance Connect Endpoint.
   - Launch the EC2 instances in the private subnets and ensure they are part of the Auto Scaling Group.
   - Set up the NAT Gateway in the public subnet to allow private instances to access the internet.
   - Configure the Application Load Balancer to distribute traffic across the EC2 instances.
   - Set up the Auto Scaling Group to manage the EC2 instances dynamically.
   - Secure the website using SSL/TLS certificates provided by AWS Certificate Manager.
   - Register the domain and set up DNS records using Route 53.

3. **Monitoring and Alerts:**

   - Configure SNS to send notifications about scaling activities and other important events.

### Accessing the Website

Once the deployment is complete, your static website will be accessible via the domain name registered through Route 53. The Application Load Balancer will handle incoming traffic and distribute it across the EC2 instances to ensure high availability.

## Repository Structure

- **/scripts:** Contains deployment scripts for setting up the infrastructure.
- **/diagrams:** Includes architectural diagrams of the AWS setup.
- **/website:** Contains the static HTML files for the website.

## License

This project is licensed under the MIT License.

---


