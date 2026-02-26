# Day 24: Setting Up an Application Load Balancer for an EC2 Instance

# Step1: Login into AWS console with the given creds

# Step2: Creating Security group

AWS Console > EC2 > Network & Security > Security Groups

#Name of SG
#Inbound rules : open HTTP port(80) for all traffic

# Step3: Creating target group

AWS Console > EC2 > Load Balancing > Target Groups

#Open port 80 for the target traffic

# Step4: Creating Application Load Balancer

AWS Console > EC2 > Load Balancing > Load Balancers > Select 'Application Load Balancer'

#Select the security group we have created, not default one
#Select the same target group as well

# Step5: Access Load Balancer in Browser

Select the Load Balancer > Copy 'DNS name(A Record)' > open the browser

# Output

Welcome to Nginx!
