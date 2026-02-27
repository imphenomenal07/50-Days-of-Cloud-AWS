# Day 25: Setting Up an EC2 Instance and CloudWatch Alarm

# Step1: Login into AWS console with the given creds

# Step2: Launch an EC2 instance with any ubuntu AMI

#Name:
#AMI: ubuntu
#Instance Type: t3.micro (free tier)
#Key pair: None

Then Launch

# Step3: Create CloudWatch Alarm

#Select Metric
- Choose : EC2 and Per-instance Metrics
- Choose Metric: CPUUtilizaton

#Configure Metric
- Static: Average
- Period: 5 Min (300 sec)

#Conditions
- Threshold type: Static
- Condition: Greater/Equal & Threshold Value: 90

#Configure SNS topic
- Select an existing SNS topic

#Alarm name: 

# Preview the tasks before submitting!!
