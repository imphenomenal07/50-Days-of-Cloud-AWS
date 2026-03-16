# Day 37: Managing EC2 Access with S3 Role-based Permissions

# Step1: Login into AWS Console

# Step2: Connect to EC2 instance via Cloud Shell

AWS Console > EC2 > Instances > Select instance 'devops-ec2' > Click on 'Connect' > User 'root' > Connect

# Step3: Create SSH keys on AWS Client and update to EC2 in Cloud Shell

#On AWS Client:

$ ssh-keygen -t rsa

$ cd .ssh

$ cat rsa_id.pub #Copy the content of file

#On Cloud Shell

$ cd .ssh

$ vi authorized_keys #Paste key content here that you copied, then save and exit!

# Step4: Create S3 bucket vi AWS Client

aws s3api create-bucket \
  --bucket devops-s3-113749894636 \
  --region us-east-1

#Expected Output:

{
    "Location": "/devops-s3-113749894636"
}

# Block public access for the bucket

aws s3api put-public-access-block \
  --bucket devops-s3-113749894636 \
  --public-access-block-configuration \
  BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true

# Verify the bucket policy

aws s3api get-public-access-block \
  --bucket devops-s3-113749894636

#Expected Output:

{
    "PublicAccessBlockConfiguration": {
        "BlockPublicAcls": true,
        "IgnorePublicAcls": true,
        "BlockPublicPolicy": true,
        "RestrictPublicBuckets": true
    }
}

# Step5: Create IAM policy

AWS Console > IAM > Policies > Create

Policy Editor: JSON

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ListBucketAccess",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::devops-s3-113749894636"
    },
    {
      "Sid": "ObjectAccess",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::devops-s3-113749894636/*"
    }
  ]
}

Policy Name and then create!!

# Step6: Create IAM role

AWS Console > IAM > Create Role

Trusted entity type: AWS service
Use Case: EC2

Select the policy that we created and then create role with the given name.

# Step7: Attach IAM role to EC2

AWS Console > EC2 > Instances > Select instance 'devops-ec2' > Actions > Security > Modify IAM role > Select the IAM role and update

# Step8: Login into EC2 via AWS Client and access s3 bucket

$ ssh root@ec2-pub-ip

#Create a empty file
$ touch file.txt

#Upload that file s3 bucket
aws s3 cp file.txt s3://devops-s3-113749894636/

#Verify the file into s3
aws s3 ls s3://devops-s3-113749894636/

# If there is any issues, troubleshoot and fix it!!
