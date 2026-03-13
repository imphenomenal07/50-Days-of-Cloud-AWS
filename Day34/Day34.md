# Day 34: Create a Lambda Function Using CLI

# Step1: Create a 'lambda_function.py' file

$ vi lambda_function.py

# Step2: Zip the 'lambda_function.py' file and verify

$ zip function.zip lambda_function.py

#Verify:

$ unzip -l function.zip

# Step3: Find out AWS Account ID

$ aws sts get-caller-identity

# Step4: Create Lambda function with required specifications

aws lambda create-function \
--function-name devops-lambda-cli \
--runtime python3.9 \
--handler lambda_function.lambda_handler \
--role arn:aws:iam::017034197451:role/lambda_execution_role \
--zip-file fileb://function.zip

#Update the AWS Account ID accordingly

# Step5: Verify the function

$ aws lambda get-function --function-name devops-lambda-cli

# Step6: Test and verify output of function

aws lambda invoke \
--function-name devops-lambda-cli \
output.json

#Verify output:

$ cat output.json

# If there is any issues, troubleshoot and fix it!!
