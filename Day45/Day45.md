# Day 45: Configure NAT Gateway for Internet Access in a Private VPC

# Step1: Login into AWS Console

# Step2: First check all the already existed resources 

# Step3: Create pub subnet with the name 'nautilus-pub-subnet'

# Step4: Create an internet gateway and attach it to private vpc

# Step5: Create Public Route Table and associate it with public subnet

Make sure public route table associated with pubic subnet and private route table associated with private subnet

# Step6: Create a NAT gateway for private subnet internet access

Edit of routes of private route table for NAT gateway with IP range 0.0.0.0/0

# Step7: Update public route table

Edit of routes of public route table for Internet gateway with IP range 0.0.0.0/0

# Step8: Once all connections are done, check resource map of private vpc to confirm

# Step9: Now open the s3 bucket and confirm text must be there!!
