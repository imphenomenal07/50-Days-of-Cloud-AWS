# Day 21: Setting Up an EC2 Instance with an Elastic IP for Application Hosting

#We are completing this task via CLI

# Step1: Create Elastic IP

aws ec2 allocate-address --domain devops-eip

# Step2: Verify the EIP and get allocation id

aws ec2 describe-addresses --filters "Name=tag:Name,Values=devops-eip" | grep "AllocationId"

# Step3: Create an EC2 instance via AWS console

# Step4: Verify and get EC2 instance id

aws ec2 describe-instances --filters "Name=tag:Name,Values=devops-ec2" | grep "InstanceId"

# Step5: Allocate EIP with the EC2

aws ec2 associate-address \
    --instance-id i-041f7b85361747a77 \
    --allocation-id eipalloc-093c490499375371f

#Expected Output:

{
    "AssociationId": "eipassoc-0aa9143f041e4c202"
}
