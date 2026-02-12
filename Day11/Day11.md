# Day 11: Attach Elastic Network Interface to EC2 Instance

# We are completing this via CLI

# Step1: Login into AWS Console with the given credentials

# Step2: Find the instance ID

aws ec2 describe-instances --filters "Name=tag:Name,Values=devops-ec2"  | grep "InstanceId"

# Step3: Finding Elastic Network Interface ID

aws ec2 describe-network-interfaces --filters "Name=tag:Name,Values=devops-eni"  | grep "NetworkInterfaceId"

# Step4: Attach Network Interface with the EC2

aws ec2 attach-network-interface \
  --network-interface-id eni-09e9e3c1cbd772494 \
  --instance-id i-0a3f5f2be9c59f824 \
  --device-index 1

# Update Instance ID and Network Interface ID

# Step5: Verify the task

aws ec2 describe-network-interfaces \
  --network-interface-ids eni-09e9e3c1cbd772494 \
  --query "NetworkInterfaces[].Attachment"

# Expected Output:

[
    {
        "AttachTime": "2026-02-12T08:10:09.000Z",
        "AttachmentId": "eni-attach-0aaf2c941ec90a8fb",
        "DeleteOnTermination": false,
        "DeviceIndex": 1,
        "NetworkCardIndex": 0,
        "InstanceId": "i-0a3f5f2be9c59f824",
        "InstanceOwnerId": "653294089478",
        "Status": "attached"
    }
]
