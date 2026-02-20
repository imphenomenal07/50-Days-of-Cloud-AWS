# Day 19: Attach IAM Policy to IAM User

# Step1: Verify the IAM user, if it is available or not

aws iam get-user --user-name iamuser_ravi

# Step2: Verify the IAM policy

aws iam list-policies \
  --scope Local \
  --query "Policies[?PolicyName=='iampolicy_ravi']"

#Expected output:

[
    {
        "PolicyName": "iampolicy_ravi",
        "PolicyId": "ANPARDXZZZKOAOWDJV446",
        "Arn": "arn:aws:iam::076759550620:policy/iampolicy_ravi",
        "Path": "/",
        "DefaultVersionId": "v1",
        "AttachmentCount": 0,
        "PermissionsBoundaryUsageCount": 0,
        "IsAttachable": true,
        "CreateDate": "2026-02-20T14:23:43Z",
        "UpdateDate": "2026-02-20T14:23:43Z"
    }
]

# Step3: Attach policy to IAM role

aws iam attach-user-policy \
  --user-name iamuser_ravi \
  --policy-arn arn:aws:iam::076759550620:policy/iampolicy_ravi

# Step4: Verify the policy is attached to user

aws iam list-attached-user-policies --user-name iamuser_ravi

#Expected Output:

{
    "AttachedPolicies": [
        {
            "PolicyName": "iampolicy_ravi",
            "PolicyArn": "arn:aws:iam::076759550620:policy/iampolicy_ravi"
        }
    ]
}
