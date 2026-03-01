# Day 27: Configuring a Public VPC with an EC2 Instance for Internet Access

# Step1: Login into AWS Console

# Step2: Create a VPC

AWS Console > Search 'VPC' > Your VPCs > Create VPC

#VPC Settings:

VPC only
Name
IPv4 CIDR

Click on 'Create VPC'

# Step2: Create a subnet

AWS Console > Search 'VPC' > Subnets > Create Subnet

VPC ID: Select the VPC that you have just created
Subnet name:
Availability Zone:
IPv4 subnet CIDR block: 

Click on 'Create Subnet'

# Step3: Enable Auto-Assign Public IP

Go to Subnets > Select your new subnet > Click Actions > Edit subnet settings > Enable and Save

# Step4: Create & Attach Internet Gateway for public access

VPC > Internet Gateways > Create internet gateway

Name:

Click Create

Select > Attach to VPC > Choose your VPC > Attach

# Step5: Step 4: Add Route to Internet

VPC > Route Tables > Select the route table associated with your subnet > Click Edit routes

Add: 0.0.0.0/0 & SAVE

# Step6: Create an EC2 instance

Inside the network settings wile creating the instance, make sure to attach the correct VPC!!

# Connect to Cloud Shell to verify SSH connections over public internet. If there is any issues, troubleshoot and fix it!!
