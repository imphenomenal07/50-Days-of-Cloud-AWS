# Day 29: Establishing Secure Communication Between Public and Private VPCs via VPC Peering

Step1: Login into AWS console

# Step2: Create a VPC Peering Connections

AWS Console > VPC > Peering Connections > Create

Name:
VPC ID (Requester): Default VPC
VPC ID (Accepter): Private VPC

Then 'Create'

# Step2: Update route tables

VPC > Route tables

Select Route table > Actions > Edit routes > Add route

Destinations: Public EC2 CIDR
Target: Peering Connection & pcx-ID

Save Changes

# Step3: Add new Inbound rule in Private EC2

SG of EC2 > Edit Inbound rule > Add new rule

Type: All ICMP - IPv4
Source: Anywhere-IPv4

# Step4: Add SSH connection in Public EC2 and connect to public EC2 via AWS Cloud shell

# Step5: Copy public RSA KEY ID to Public EC2 in Cloud Shell

$ cat .ssh/rsa_id.pub #Copy content

#Go to Cloud shell and paste

$ vi .ssh/authorized_keys

# Step6: Now login into public ec2 via kke terminal and ping private ec2

$ ssh ec2-user@public-ip-of-public-ec2

#Once connected, ping private ec2 via private IPv4

$ ping private-ip-of-private-ec2
