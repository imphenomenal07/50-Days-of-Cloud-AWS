# Day 48: Automating Infrastructure Deployment with AWS CloudFormation

# Step1: Create a CloudFormation Template

$ vi nautilus-lambda.yml

#File Content:

AWSTemplateFormatVersion: '2010-09-09'
Description: Nautilus Lambda Application Stack

Resources:

  LambdaExecutionRole:
    Type: AWS::IAM::Role
    Properties:
      RoleName: lambda_execution_role
      AssumeRolePolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Principal:
              Service: lambda.amazonaws.com
            Action: sts:AssumeRole
      ManagedPolicyArns:
        - arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole

  NautilusLambdaFunction:
    Type: AWS::Lambda::Function
    Properties:
      FunctionName: nautilus-lambda
      Runtime: python3.9
      Handler: index.lambda_handler
      Role: !GetAtt LambdaExecutionRole.Arn
      Timeout: 10
      Code:
        ZipFile: |
          def lambda_handler(event, context):
              return {
                  "statusCode": 200,
                  "body": "Welcome to KKE AWS Labs!"
              }

#Save and exit. Make sure to update file as per task!!

# Step2: Create CloudFormation stack

aws cloudformation create-stack \
  --stack-name nautilus-lambda-app \
  --template-body file:///root/nautilus-lambda.yml \
  --capabilities CAPABILITY_NAMED_IAM

#Expected Output:

{
    "StackId": "arn:aws:cloudformation:us-east-1:127822742629:stack/nautilus-lambda-app/df145580-30bd-11f1-95a0-0affe8577d8d"
}

# Step3: Wait for task completion

aws cloudformation wait stack-create-complete \
  --stack-name nautilus-lambda-app

# Step4: Test/Invoke the Lambda function

aws lambda invoke \
  --function-name nautilus-lambda \
  output.json

#Expected Output:

{
    "StatusCode": 200,
    "ExecutedVersion": "$LATEST"
}

# Step5: Verify the output

$ cat output.json

#Expected Output:

{"statusCode": 200, "body": "Welcome to KKE AWS Labs!"}
