# Day 42: Building and Managing NoSQL Databases with AWS DynamoDB

# Step1: Login into AWS Console

# Step2: Create DynamoDB table

AWS Console > Search for 'DynamoDB' > Create table

Table name:

Partition key: key-name & Select 'String'

Create table

# Step3: Insert task items

Open table 'nautilus-tasks' > Explore table items > Create item > json view

#Task1:

{
  "taskId": { "S": "1" },
  "description": { "S": "Learn DynamoDB" },
  "status": { "S": "completed" }
}

#Task2:

{
  "taskId": { "S": "2" },
  "description": { "S": "Build To-Do App" },
  "status": { "S": "in-progress" }
}

# Step4: Verify the task items

Run the task and verify status!!
