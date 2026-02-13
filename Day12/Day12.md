# Day 12: Attach Volume to EC2 Instance

# We are completing this via CLI

# Step1: Login into AWS Console with the given credentials

# Step2: Find the instance ID

aws ec2 describe-instances --filters "Name=tag:Name,Values=nautilus-ec2"  | grep "InstanceId"

# # Step3: Finding Elastic Volume ID

aws ec2 describe-volumes --filters "Name=tag:Name,Values=nautilus-volume"  | grep "VolumeId"

# # Step4: Attaching Elastic Volume with the EC2

aws ec2 attach-volume \
  --volume-id vol-0c71fe0b6b65b6e72 \
  --instance-id i-054de77c39e13f081 \
  --device /dev/sdb

# Expected Output:

{
    "VolumeId": "vol-0c71fe0b6b65b6e72",
    "InstanceId": "i-054de77c39e13f081",
    "Device": "/dev/sdb",
    "State": "attaching",
    "AttachTime": "2026-02-13T07:17:10.559Z"
}

# Step5: Verify the task

aws ec2 describe-volumes \
  --volume-ids vol-0c71fe0b6b65b6e72 \
  --query "Volumes[].Attachments"

# Expected output:

[
    [
        {
            "DeleteOnTermination": false,
            "VolumeId": "vol-0c71fe0b6b65b6e72",
            "InstanceId": "i-054de77c39e13f081",
            "Device": "/dev/sdf",
            "State": "attached",
            "AttachTime": "2026-02-13T07:17:10.000Z"
        }
    ]
]
