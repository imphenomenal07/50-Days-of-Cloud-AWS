# Day 30: Enable Internet Access for Private EC2 using NAT Instance

# Step1: Login into AWS console and check all the mentioned things must be available there!!

# Step2: Create a public with the Private VPC

VPC Dashboard > Subnet > Create Sublet:

Select the Private VPC
Name of Subnet

Create

# Step2: Enable auto assign IPv4 for Public Subnet

Subnet > Select 'Public Subnet' > Actions > Edit Subnet Settings > Click 'Enable auto-assign public IPv4 address' > Save

# Step3: Create Internet Gateway for Public access

VPC > Internet Gateways > Create Internet Gateway

Name:

Then 'Create Internet Gateway'

# Step4: Attach Internet Gateway to Private VPC

Select the IGW > Actions > Attach to VPC 'Select Private VPC'

# Step5: Edit Route Table of Public subnet

VPC > Click on 'Private VPC' > Public Route table > Edit Routes

Destination: 0.0.0.0/0
Target: Internet Gateway
Select the IGW and Save

# Step6: Create a NAT EC2 instance

Networking: Select Private VPC and Public Subnet

#Make sure to use the custom security group and add SSH  & all traffic rule in same SG


# Step7: Disable Source/Destination Check

Select 'nautilus-nat-instance' > Actions > Networking > Change source/destination check > Disable it > Save

# Step8: Edit Route Table of Public subnet

Destination: 0.0.0.0/0
Target: Instance
Select the Instance and Save

# Step9: Enable IP Forwarding on NAT Instance

#Connect to cloud shell with the NAT instance and execute below commands

$ sudo yum install iptables-services
$ sysctl net.ipv4.ip_forward
$ sudo sysctl -w net.ipv4.ip_forward=1
$ sysctl net.ipv4.ip_forward
$ sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
$ sudo service iptables save

# Step10: Check the file is updated in the mentioned s3 bucket. If not, wait and update it again!!
