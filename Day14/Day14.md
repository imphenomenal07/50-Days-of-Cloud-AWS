# Day 14: Terminate EC2 Instance

# We are completing this via CLI

# Step1: Find the instance ID

aws ec2 describe-instances --filters "Name=tag:Name, Values=xfusion-ec2"  | grep "InstanceId"

# Step2: Terminate the instance

aws ec2 terminate-instances --instance-ids i-048b4928b9455b5a5

# Step3: Wait Until Fully Terminated (OPTIONAL)

aws ec2 wait instance-terminated --instance-ids i-048b4928b9455b5a5

# Step4: Verify the instance state

aws ec2 describe-instances \
  --instance-ids i-048b4928b9455b5a5 \
  --query "Reservations[].Instances[].State.Name" \
  --output text

# Expected Output

Terminated
