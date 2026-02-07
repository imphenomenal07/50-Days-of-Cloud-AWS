# Day 6: Launch EC2 Instance

# Step1: Login into AWS console with the given credentails
# Step2: Go to EC2 Dashboard and launch an instance

Search 'EC2' > Instances > Launch Instance

#Name: name-of-instance
#AMI: Amazon Linux
#Instance-type: t2.micro
#Key pair: create key-pair with the given name & select the same key-pair
#Secuirty-group: Click on 'Select on Existing group' & select the default security-group

#View Summary and finaly Launch the Instance

# Step3: Go back to terminal and run below command to verify
$ aws ec2 describe-instances
