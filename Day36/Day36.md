# Day 36: Load Balancing EC2 Instances with Application Load Balancer

# Step1: Login into AWS Console

# Step2: Create a new SG

AWS Console > EC2 > Security Groups > Create Security group

Add 'Inbound Rule' for SSH, HTTP and All Traffic

# Step3: Create EC2 instance including 'user data'

AWS Console > EC2 > Instances > Create Instance

Select Group (that one was created newly)

Advance Settings > User Data

#!/bin/bash

sudo apt update -y
sudo apt install nginx -y
sudo systemctl start nginx && sudo systemctl enable nginx


Then 'Launch Instance'

# Step4: Create Target group

AWS Console > EC2 > Load Balancing > Target Groups > Create target group

Type: Instance

Register Targets -> Select the instance that we have created

# Step5: Create a Application Load Balancer

AWS Console > EC2 > Load Balancing > Create load balancer > Application Load Balancer > Create

Name:
Scheme: Internet-facing
LB IP address type: IPv4

VPC: default

AZ and subnets: make sure to select the correct Availability zones in which instance is created

Security Group: default

Listeners and Routing:
       Protocol: HTTP
       Port: 80

       Routing Action: Forward to target groups
       Target Group: Select the 'target group'

Then 'Create load balancer'

# Wait for 3-4 mins until ALB becomes in active, then copy the ALB DNS and paste in browser to check if nginx service is accessible or not. If not, troubleshoot and fix it!!
