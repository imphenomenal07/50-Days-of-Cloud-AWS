# Day 9: Enable Termination Protection for EC2 Instance

# Step1: Login into AWS Console with the given credentials

# Step2: Open EC2 dashboard

AWS Console > Search 'EC2' > Open EC2 Dashbaord > Instances > Select the running isntance > Actions > Instance Settings > Change Termination Protection > Click on 'Enabled' > Save

# Step3: Go back to terminal and verify

$ aws ec2 describe-instances | grep "InstanceId"

# Check API status

aws ec2 describe-instance-attribute \
  --instance-id i-0785a90ba069744a3 \
  --attribute disableApiTermination

#Change instance id with your instance id

# Expected Output

{
    "DisableApiTermination": {
        "Value": true
    }
}
