# Day 20: Create IAM Role for EC2 with Policy Attachment

# Step1: Create a trust policy for IAM role

$ vi role-policy.json

#File Content:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}

# Step2: Create the IAM role

aws iam create-role \
  --role-name iamrole_anita \
  --assume-role-policy-document file://role-policy.json

# Step3: Verify the IAM policy available or not

aws iam list-policies \
  --scope Local \
  --query "Policies[?PolicyName=='iampolicy_anita']"

# If policy is not created, then create one

$ vi policy.json

#File Content:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}

# Create IAM Policy

aws iam create-policy \
    --policy-name iampolicy_anita \
    --policy-document file://policy.json

# Step4: Attached IAM policy to the IAM role

aws iam attach-role-policy \
  --role-name iamrole_anita \
  --policy-arn arn:aws:iam::527951558168:policy/iampolicy_anita

# Step5: Verify if policy attached to the role

aws iam list-attached-role-policies \
  --role-name iamrole_anita

#Expected Output:

{
    "AttachedPolicies": [
        {
            "PolicyName": "iampolicy_anita",
            "PolicyArn": "arn:aws:iam::527951558168:policy/iampolicy_anita"
        }
    ]
}
