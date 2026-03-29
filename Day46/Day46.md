# Day 46: Event-Driven Processing with Amazon S3 and Lambda

# Step1: Login into AWS Console

# Step2: Create a public s3 bucket

AWS Console > s3 > Create bucket

Uncheck 'Block all public access'

#Add below bucket policy:

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::devops-public-4315/*"
        }
    ]
}

# Step3: Create private s3 bucket

AWS Console > s3 > Create bucket

Make sure 'Block all public access' box must be checked

# Step4: Create DynamoDB table

AWS Console > DynamoDB > Create table

Name:
Partition Key: KeyID (String)

# Step5: Create iam-role 'lambda_execution_role' and attach below policies

AWSLambdaBasicExecutionRole
AmazonS3FullAccess
AmazonDynamoDBFullAccess

# Step6: Update Lambda Code on AWS Client

$ vi lambda-function.py

#Replace the below values:

DYNAMODB_TABLE = "dynamodb-table-name"
DESTINATION_BUCKET = "private-s3-bucket-name"

# Step7: Create Lambda function

AWS Console > Lambda > Create function

Function Name:
Runtime: Python 3.9
Execution role: Use existing role
Role: lambda_execution_role

Copy the code from 'lambda-function.py' and paste in Lambda code editor

Create function and Deploy

# Step8: Add triggers in Lambda function

Open Function > Add triggers

Select 's3' > select 's3-publuc-bucket'

Event type: PUT
Acknowledge permission prompt

Add

# Step9: Copy file to public s3 bucket

$ aws s3 cp /root/sample.zip s3://devops-public-4315/

# Step10: Verify the task
Make sure same file must be available in private s3 bucket. Also check logs of DynamoDB table!!
