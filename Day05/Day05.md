# Day 5: Create GP3 Volume

# Step1: Login into AWS console with the given credentials
# Step2: Search 'EC2' and open EC2 dashboard

EC2 > Elastic Block Storage > Volumes > Create Volumes

# Add Tags in key-valaue pairs
#Key: Name
#Value: name-of-volume

# Also configure volume size as per requirement

# Step3: Go back to terminal and run below command to verify
$ aws ec2 describe-volumes
