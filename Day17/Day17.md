# Day 17: Create IAM Group

# We are completing this task via CLI

# Step1: Create IAM group

aws iam create-group --group-name iamgroup_kareem

# Expected Output:

{
    "Group": {
        "Path": "/",
        "GroupName": "iamgroup_kareem",
        "GroupId": "AGPATYGLDV56YQVWSFAGZ",
        "Arn": "arn:aws:iam::258124001149:group/iamgroup_kareem",
        "CreateDate": "2026-02-18T06:28:49Z"
    }
}

# Step2: Verify group

aws iam get-group --group-name iamgroup_kareem

# Expected Output:

{
    "Users": [],
    "Group": {
        "Path": "/",
        "GroupName": "iamgroup_kareem",
        "GroupId": "AGPATYGLDV56YQVWSFAGZ",
        "Arn": "arn:aws:iam::258124001149:group/iamgroup_kareem",
        "CreateDate": "2026-02-18T06:28:49Z"
    }
}

# To list all the groups

aws iam list-groups

#It will list all the groups!!
