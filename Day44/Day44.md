# Day 44: Implementing Auto Scaling for High Availability in AWS

# Step1: Login to AWS Console

# Step2: Create EC2 Launch Template

AWS Console > EC2 > Launch Templates > Create launch template

Name:
AMI: Amazon Linux 2
Instance Type: t2.micro

Security Group: Create new SG and open port 80


Advance details > User Data

#!/bin/bash

sudo yum update -y
sudo yum install nginx -y
sudo systemctl start nginx && sudo systemctl enable nginx

Create launch template

# Step3: Create Auto Scaling group

EC2 > Auto Scaling Groups > Create Auto Scaling group

Name:
Launch template:

Next

Availability Zones and subnets: Select a, b & c

Next

Load Balancing: No Load Balancer (Just for now)

Next

Desired Capacity type:

Min desired capacity:
Max desired capacity:

Next, Review and Create Auto Scaling group

# Step4: Create Target groups

EC2 > Load Balancing > Target Groups > Create target group

Target type: Instances

Target group name:

Next > Select Instance > Review > Create target group

# Step5: Create Applications Load Balancer

EC2 > Load Balancing > Load Balancers > Create Load Balancer

Load Balancer Type: Applications Load Balancer

Name:
Scheme: Internet-facing
IP Type: IPv4

Availability Zones and subnets: a, b & c (that we used in creating AGS)

Security groups: the one we used in creating AGS

Target group: the one we just created

Create load balancer

# Step6: Attach the ALB to ASG

Select the ASG > Actions > Edit > Load balancing

Click on 'Application, Network or Gateway Load Balancer target groups' 

And select the required target group & update

# Step7: Access the nginx web service

Copy the DNS of ALB and open it new tab!!
