# AWS Three Tier Web Architecture Workshop

## Description: 
This hands-on workshop guides you through building a highly available and scalable three-tier web architecture in AWS. We will manually create and configure the necessary network, security, application, and database components to implement this architecture.
![543c80b3-dc70-45de-8988-c194498c4967](https://github.com/user-attachments/assets/c1945c8b-0acd-411b-b165-cab01390c1da)

Architecture Highlights:
A public-facing Application Load Balancer routes client traffic to the web tier EC2 instances running Nginx web servers.
The web tier serves a React.js website and redirects API calls to the internal-facing load balancer of the application tier.
The application tier, built with Node.js, processes API calls, interacts with an Aurora MySQL Multi-AZ database, and returns data to the web tier.
Load balancing, health checks, and autoscaling groups are configured at each layer to maintain high availability and scalability.

Step-by-Step Algorithm

Step 1: Download Code from GitHub
Clone the repository to your local system to access the necessary application code.

Step 2: Create S3 Buckets
Create one S3 bucket for storing the web-server and app-server code.
Upload the application code to this S3 bucket.
Create another S3 bucket to store VPC flow logs.

Step 3: Set Up IAM Role with Required Policies
Attach policies:
AmazonS3ReadOnlyAccess
AmazonSSMManagedInstanceCore

Step 4: Build the Network Infrastructure
Create a VPC, public/private subnets, an Internet Gateway (IGW), a NAT Gateway (NAT-GW), and appropriate Route Tables (RT).
Enable auto-assignment of public IPs for web-tier public subnets.
Configure flow logs for the VPC, directing them to the designated S3 bucket.

Step 5: Configure Security Groups
External Load Balancer SG: Allow HTTP (80) from 0.0.0.0/0.
Web-Tier SG: Allow HTTP from the External Load Balancer SG.
Internal Load Balancer SG: Allow HTTP from the Web-Tier SG.
App-Tier SG: Allow port 4000 from the Internal Load Balancer SG.
DB-Tier SG: Allow MySQL (3306) from the App-Tier SG.

Step 6: Set Up Database Layer
Create a DB subnet group.
Deploy an Aurora MySQL Multi-AZ RDS instance in the DB subnet group.

Step 7: Configure and Test the Application Tier
Launch a test app server and install required packages.
App Server Commands
Test connections and create an AMI.
Create a launch template using the AMI.
Set up a target group and an internal load balancer.
Configure an autoscaling group.
Edit the nginx.conf file locally, adding the Internal-LB-DNS, and upload it to S3.

Step 8: Configure and Test the Web Tier
Launch a test web server and install required packages:
Nginx
Node.js (for React.js).
Web Server Commands
Test connections and create an AMI.
Create a launch template using the AMI.
Set up a target group and an external load balancer.
Configure an autoscaling group.

Step 9: Implement Monitoring and Logging
Configure CloudWatch Alarms and integrate them with SNS notifications.
Set up CloudTrail to monitor API calls and resource usage.
