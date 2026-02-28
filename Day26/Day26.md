# Day 26: Configuring an EC2 Instance as a Web Server with Nginx

# Step1: Login into AWS console

# Step2: Create an EC2 instance

#Name: 

#AMI: Ubuntu(any)

#Instance type: free tier eligible

#Key Pair Name: Proceed without a key pair

#Network Settings: Allow SSH and HTTP traffic from internet

#Advance details:

User Data:

#!/bin/bash
apt update -y
apt install -y nginx
systemctl start nginx
systemctl enable nginx

And Launch instance

# Step3: Access nginx server

-  Wait for few mins until instance passes all the health checks
- Copy Public Ip address of instance and paste in browser
- If nginx not running, refresh the page or trouble the instance configurations!!
