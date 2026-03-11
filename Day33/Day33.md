# Day 33: Create a Lambda Function

# Step1:Login to AWS Console

# Step2: Create a IAM role for the same

AWS Console > IAM > Roles > Create role

# Step3: Create Lambda Function

AWS Console > Lambda > Functions > Create Function

Author from scratch
Function Name
Runtime: Python 3.xx

Execution role > Use another role > Select the required role > Create function

# Step4: Update the editor code

import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Welcome to KKE AWS Labs!'
    }

# Step5: Deploy code and Test the code!!
