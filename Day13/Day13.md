# Day 13: Create AMI from EC2 Instance

# We are completing this via CLI

# Step1: Find the instance ID

aws ec2 describe-instances --filters "Name=tag:Name,Values=nautilus-ec2"  | grep "InstanceId"

# Step2: Create the image with the ec2 instance

aws ec2 create-image \
  --instance-id i-0c58d0ebaacf195c9 \
  --name "xfusion-ec2-ami" \
  --no-reboot

# Expected output:

{
    "ImageId": "ami-066a6de57a984bdbb"
}

# Step3: Verify the AMI image with the table format

aws ec2 describe-images --owners self --query 'Images[*].[ImageId,Name,State]' --output table

# Expected Output:

|                     DescribeImages                      |
+------------------------+-------------------+------------+
|  ami-066a6de57a984bdbb |  xfusion-ec2-ami  |  available

# or get output in json format

aws ec2 describe-images --owners self --query 'Images[*].[ImageId,Name,State]' --output json

# Expected output:

[
    [
        "ami-066a6de57a984bdbb",
        "xfusion-ec2-ami",
        "available"
    ]
]
