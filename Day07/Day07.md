# Day 7: Change EC2 Instance Type

# Step1: Login into AWS console with the given credentails
# Step2: Search and open 'EC2' dashboard
# Step3: Stop the instance type

#Select the instance > Instance state > Stop Instance

# Step4: Change instance type

#Select Instance > Actions > Instance Settings > Change instance type > Remove the old instance & update the new one > Save

# Step5: Restart the instnace

#Refresh the page > Select instnace > Instance state > start instance

# Step6: Go back to terminal and run below command to verify

$ aws ec2 describe-instances | grep "InstanceType"
