# Day 47: Integrating AWS SQS and SNS for Reliable Messaging

# Step1: Create Stack YML file

$ vi xfusion-priority-stack.yml

#File Content:

AWSTemplateFormatVersion: '2010-09-09'
Description: >
  xfusion Priority Queuing System using Amazon SQS, SNS, and Lambda.
  Uses only AWS managed policies.

Resources:
  # IAM Role
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
        - arn:aws:iam::aws:policy/AmazonSQSFullAccess
        - arn:aws:iam::aws:policy/AmazonSNSFullAccess

  # SQS Queues
  xfusionHighPriorityQueue:
    Type: AWS::SQS::Queue
    Properties:
      QueueName: xfusion-High-Priority-Queue
      VisibilityTimeout: 30
      MessageRetentionPeriod: 86400

  xfusionLowPriorityQueue:
    Type: AWS::SQS::Queue
    Properties:
      QueueName: xfusion-Low-Priority-Queue
      VisibilityTimeout: 30
      MessageRetentionPeriod: 86400

  # SQS Queue Policies
  xfusionHighPriorityQueuePolicy:
    Type: AWS::SQS::QueuePolicy
    Properties:
      Queues:
        - !Ref xfusionHighPriorityQueue
      PolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Principal:
              Service: sns.amazonaws.com
            Action: sqs:SendMessage
            Resource: !GetAtt xfusionHighPriorityQueue.Arn
            Condition:
              ArnEquals:
                aws:SourceArn: !Ref xfusionPriorityQueuesTopic

  xfusionLowPriorityQueuePolicy:
    Type: AWS::SQS::QueuePolicy
    Properties:
      Queues:
        - !Ref xfusionLowPriorityQueue
      PolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Principal:
              Service: sns.amazonaws.com
            Action: sqs:SendMessage
            Resource: !GetAtt xfusionLowPriorityQueue.Arn
            Condition:
              ArnEquals:
                aws:SourceArn: !Ref xfusionPriorityQueuesTopic

  # SNS Topic
  xfusionPriorityQueuesTopic:
    Type: AWS::SNS::Topic
    Properties:
      TopicName: xfusion-Priority-Queues-Topic

  # SNS Subscriptions (with Filters)
  HighPrioritySubscription:
    Type: AWS::SNS::Subscription
    Properties:
      TopicArn: !Ref xfusionPriorityQueuesTopic
      Protocol: sqs
      Endpoint: !GetAtt xfusionHighPriorityQueue.Arn
      FilterPolicy:
        priority:
          - high

  LowPrioritySubscription:
    Type: AWS::SNS::Subscription
    Properties:
      TopicArn: !Ref xfusionPriorityQueuesTopic
      Protocol: sqs
      Endpoint: !GetAtt xfusionLowPriorityQueue.Arn
      FilterPolicy:
        priority:
          - low

  # Lambda Function
  xfusionPrioritiesQueueFunction:
    Type: AWS::Lambda::Function
    Properties:
      FunctionName: xfusion-priorities-queue-function
      Runtime: python3.12
      Handler: index.lambda_handler
      Role: !GetAtt LambdaExecutionRole.Arn
      Timeout: 60
      MemorySize: 128
      Environment:
        Variables:
          high_priority_queue: !Ref xfusionHighPriorityQueue
          low_priority_queue: !Ref xfusionLowPriorityQueue
      Code:
        ZipFile: |
          import boto3
          import os
          sqs = boto3.client('sqs')
          def delete_message(queue_url, receipt_handle, message):
              response = sqs.delete_message(QueueUrl=queue_url, ReceiptHandle=receipt_handle)
              return "Message " + "'" + message + "'" + " deleted"

          def poll_messages(queue_url):
              QueueUrl=queue_url
              response = sqs.receive_message(
                  QueueUrl=QueueUrl,
                  AttributeNames=[],
                  MaxNumberOfMessages=1,
                  MessageAttributeNames=['All'],
                  WaitTimeSeconds=3
              )
              if "Messages" in response:
                  receipt_handle=response['Messages'][0]['ReceiptHandle']
                  message = response['Messages'][0]['Body']
                  delete_response = delete_message(QueueUrl,receipt_handle,message)
                  return delete_response
              else:
                  return "No more messages to poll"

          def lambda_handler(event, context):
              response = poll_messages(os.environ['high_priority_queue'])
              if response == "No more messages to poll":
                  response = poll_messages(os.environ['low_priority_queue'])
              return response

#Save and exit from file. Make sure to update YML file as per task

# Step2: Create CloudFormation stack

aws cloudformation create-stack \
  --stack-name xfusion-priority-stack \
  --template-body file:///root/xfusion-priority-stack.yml \
  --capabilities CAPABILITY_NAMED_IAM

#Expected Output:

{
    "StackId": "arn:aws:cloudformation:us-east-1:026563957752:stack/xfusion-priority-stack/8b245bd0-2fe8-11f1-9b51-12196f819c81"
}

# Step3: Wait till to complete the task

$ aws cloudformation wait stack-create-complete --stack-name xfusion-priority-stack

# Step4: Invoke Lambda function

aws lambda invoke --function-name xfusion-priorities-queue-function --payload '{}' response.json && cat response.json

#Expected output:

{
    "StatusCode": 200,
    "ExecutedVersion": "$LATEST"
}
"No more messages to poll"

# Step5: Publish Test Messages as given in task

topicarn=$(aws sns list-topics --query "Topics[?contains(TopicArn, 'nautilus-Priority-Queues-Topic')].TopicArn" --output text)
aws sns publish --topic-arn $topicarn --message 'High Priority message 1' --message-attributes '{"priority" : { "DataType":"String", "StringValue":"high"}}'
aws sns publish --topic-arn $topicarn --message 'High Priority message 2' --message-attributes '{"priority" : { "DataType":"String", "StringValue":"high"}}'
aws sns publish --topic-arn $topicarn --message 'Low Priority message 1' --message-attributes '{"priority" : { "DataType":"String", "StringValue":"low"}}'
aws sns publish --topic-arn $topicarn --message 'Low Priority message 2' --message-attributes '{"priority" : { "DataType":"String", "StringValue":"low"}}'

#Expected Output:

Will receive priority task IDs accordingly!!
