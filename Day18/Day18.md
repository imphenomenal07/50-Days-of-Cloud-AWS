# Day 18: Create Read-Only IAM Policy for EC2 Console Access

#We are doing this this via CLI mode

# Step1: Create a json file and describe the policy roles

$ vi ravi-policy.json

#Policy

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "EC2ReadOnlyAccess",
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:DescribeImages",
        "ec2:DescribeSnapshots",
        "ec2:DescribeVolumes",
        "ec2:DescribeTags",
        "ec2:DescribeSecurityGroups",
        "ec2:DescribeKeyPairs",
        "ec2:DescribeNetworkInterfaces",
        "ec2:DescribeSubnets",
        "ec2:DescribeVpcs",
        "ec2:DescribeRegions",
        "ec2:DescribeAvailabilityZones"
      ],
      "Resource": "*"
    }
  ]
}

# Step2: Create the IAM policy

aws iam create-policy \
    --policy-name iampolicy_ravi \
    --policy-document file://ravi-policy.json

#Expected Output:

{
    "Policy": {
        "PolicyName": "iampolicy_ravi",
        "PolicyId": "ANPASMGZ6BNEAJ7OLFVH6",
        "Arn": "arn:aws:iam::163665808200:policy/iampolicy_ravi",
        "Path": "/",
        "DefaultVersionId": "v1",
        "AttachmentCount": 0,
        "PermissionsBoundaryUsageCount": 0,
        "IsAttachable": true,
        "CreateDate": "2026-02-19T08:42:15Z",
        "UpdateDate": "2026-02-19T08:42:15Z"
    }
}

# Step2: Verify the policy

aws iam list-policies --scope Local

#Expected Output:

{
    "Policies": [
        {
            "PolicyName": "iampolicy_ravi",
            "PolicyId": "ANPASMGZ6BNEAJ7OLFVH6",
            "Arn": "arn:aws:iam::163665808200:policy/iampolicy_ravi",
            "Path": "/",
            "DefaultVersionId": "v1",
            "AttachmentCount": 0,
            "PermissionsBoundaryUsageCount": 0,
            "IsAttachable": true,
            "CreateDate": "2026-02-19T08:42:15Z",
            "UpdateDate": "2026-02-19T08:42:15Z"
        },
        {
            "PolicyName": "AWSIAMWithDateConditionsNewConstraints",
            "PolicyId": "ANPASMGZ6BNEJTPAHVPMT",
            "Arn": "arn:aws:iam::163665808200:policy/AWSIAMWithDateConditionsNewConstraints",
            "Path": "/",
            "DefaultVersionId": "v1",
            "AttachmentCount": 1,
            "PermissionsBoundaryUsageCount": 0,
            "IsAttachable": true,
            "CreateDate": "2026-02-19T08:18:10Z",
            "UpdateDate": "2026-02-19T08:18:10Z"
        },
        {
            "PolicyName": "AWSIAMWithDateConditions",
            "PolicyId": "ANPASMGZ6BNEPGT73V5QC",
            "Arn": "arn:aws:iam::163665808200:policy/AWSIAMWithDateConditions",
            "Path": "/",
            "DefaultVersionId": "v1",
            "AttachmentCount": 1,
            "PermissionsBoundaryUsageCount": 0,
            "IsAttachable": true,
            "CreateDate": "2026-02-19T08:18:10Z",
            "UpdateDate": "2026-02-19T08:18:10Z"
        }
    ]
}
