
# Static Website Hosting on AWS

This project demonstrates how to host a static HTML web app on AWS, leveraging a range of AWS services to ensure scalability, security, and high availability. The entire infrastructure is described using the following AWS resources.

## Architecture Overview

The architecture for this project includes the following key components:

1. **Virtual Private Cloud (VPC)**: A custom VPC was configured with both public and private subnets across two different availability zones to ensure high availability and fault tolerance.

2. **Internet Gateway**: An Internet Gateway was deployed to enable communication between instances within the VPC and the broader internet.

3. **Security Groups**: Network firewall security groups were established to control inbound and outbound traffic to resources within the VPC.

4. **Availability Zones**: Two availability zones were utilized to enhance system reliability and fault tolerance.

5. **Public Subnets**: Public subnets were utilized for infrastructure components like the NAT Gateway and Application Load Balancer.

6. **EC2 Instance Connect Endpoint**: This was implemented for secure access to assets in both public and private subnets.

7. **Private Subnets**: Web servers (EC2 instances) were positioned within private subnets for enhanced security.

8. **NAT Gateway**: Instances in private subnets were configured to access the internet through the NAT Gateway.

9. **EC2 Instances**: The static website was hosted on EC2 instances.

10. **Application Load Balancer (ALB)**: An ALB was employed to evenly distribute web traffic to an Auto Scaling Group of EC2 instances across multiple availability zones.

11. **Auto Scaling Group (ASG)**: An ASG was used to manage EC2 instances automatically, ensuring website availability, scalability, fault tolerance, and elasticity.

12. **GitHub**: The website files were stored on GitHub for version control and collaboration.

13. **AWS Certificate Manager**: SSL/TLS certificates were used to secure communications for the application.

14. **Simple Notification Service (SNS)**: SNS was configured to send alerts regarding activities within the Auto Scaling Group.

15. **Route 53**: A domain name was registered and DNS records were set up using Route 53 for the website.

## Deployment

Follow these steps to deploy the static HTML web app on an EC2 instance:

1. **Launch an EC2 Instance**:
    - Choose an Amazon Linux 2 AMI in one of your private subnets.
    - Ensure that the instance has a security group allowing HTTP (port 80) traffic from the ALB.
    
2. **SSH into the EC2 Instance**:
    - Use EC2 Instance Connect or an SSH client to access your EC2 instance.
  
3. **Run the Deployment Script**:
    - Switch to the root user to gain full administrative privileges:
      ```bash
      sudo su
      ```
    - Update all installed packages to their latest versions:
      ```bash
      yum update -y
      ```
    - Install Apache HTTP Server:
      ```bash
      yum install -y httpd
      ```
    - Navigate to the Apache web root:
      ```bash
      cd /var/www/html
      ```
    - Install Git:
      ```bash
      yum install git -y
      ```
    - Clone the project repository from GitHub:
      ```bash
      git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
      ```
    - Copy all files, including hidden ones, to the Apache web root:
      ```bash
      cp -R host-a-static-website-on-aws/. /var/www/html/
      ```
    - Remove the cloned repository directory to clean up unnecessary files:
      ```bash
      rm -rf host-a-static-website-on-aws
      ```
    - Enable the Apache HTTP Server to start automatically at system boot:
      ```bash
      systemctl enable httpd
      ```
    - Start the Apache HTTP Server to serve the web content:
      ```bash
      systemctl start httpd
      ```

## Repository

All the necessary deployment scripts and the reference architecture diagram can be found in the [GitHub repository](https://github.com/aosnotes77/host-a-static-website-on-aws).

## Conclusion

This project successfully demonstrates how to host a static HTML website on AWS by leveraging a range of AWS services to ensure a secure, scalable, and highly available web application infrastructure.

---




