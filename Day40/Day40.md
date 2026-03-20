# Day 40: Troubleshooting Internet Accessibility for an EC2-Hosted Application

# Step1: Login into AWS Console

# Step2: Check if port 80 [HTTP] is configured in the required Security Group

# Step3: Also add port 22 [SSH] into the same SG for Cloud Shell Connection

# Step4: Check the VPC connections, all resources should be shown connected

devops-vpc -> devops-subnet -> devops-rt[Route Table] -> devops-ig[Internet Gateway]

# Step5: Internet gateway is not attached to VPC, make sure to attach it properly

VPC > Internet gateways > Select required Internet Gateway > Actions > Attach to VPC

# Step6: Update route table to make Instance publicly accessible

VPC > Route tables > click on req. RT > edit routes > Add route

Destination: 0.0.0.0/8
Target: Instance and select required instance

Save changes

# Step7: Connect to instance via Cloud Shell to check nginx status

AWS Console > EC2 > Select Instance > Connect

#Check instance status once connected

$ sudo systemctl status nginx

#Make sure nginx enabled and running. If not, enable and start the nginx

$ sudo systemctl enable ngnix && sudo systemctl start nginx && sudo systemctl status nginx

# Step8: Check EC2 instance connection

Copy public IP and open in browser (http://ec2-pub-ip)
