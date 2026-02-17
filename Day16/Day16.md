# Day 16: Create IAM User

#We are completing this task via CLI

# Step1: Create IAM user

aws iam create-user --user-name iamuser_jim

# Expected Output:

{
    "User": {
        "Path": "/",
        "UserName": "iamuser_jim",
        "UserId": "AIDA2NAEWZZ5XTEDHHW4T",
        "Arn": "arn:aws:iam::715121938043:user/iamuser_jim",
        "CreateDate": "2026-02-17T06:44:54Z"
    }
}

# Step2: Verify user

aws iam get-user --user-name iamuser_jim

# Expected Output:

{
    "User": {
        "Path": "/",
        "UserName": "iamuser_jim",
        "UserId": "AIDA2NAEWZZ5XTEDHHW4T",
        "Arn": "arn:aws:iam::715121938043:user/iamuser_jim",
        "CreateDate": "2026-02-17T06:44:54Z"
    }
}

# To list all IAM users

aws iam list-users

# Expected Output:

{
    "Users": [
        {
            "Path": "/",
            "UserName": "iamuser_jim",
            "UserId": "AIDA2NAEWZZ5XTEDHHW4T",
            "Arn": "arn:aws:iam::715121938043:user/iamuser_jim",
            "CreateDate": "2026-02-17T06:44:54Z"
        },
        {
            "Path": "/",
            "UserName": "kk_labs_user_766859",
            "UserId": "AIDA2NAEWZZ54Z2QK7G5S",
            "Arn": "arn:aws:iam::715121938043:user/kk_labs_user_766859",
            "CreateDate": "2026-02-17T03:28:47Z"
        }
    ]
}
