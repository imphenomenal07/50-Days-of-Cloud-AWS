# Day 39: Hosting a Static Website on AWS S3

# Step1: Login into AWS Console

# Step2: Create a public bucket

AWS Console > S3 > Create Bucket

Bucket type: General purpose
Bucket name: 

Object Ownership: ACLs disabled

Block all public access: uncheck the box

Create bucket

# Step3: Update the bucket policy

Open bucket > Permissions > Bucket policy > Edit > Paste the below content in editor and Save

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::xfusion-web-14165/*"
    }
  ]
}

#Make sure to update the Resource section with your bucket arn!!

# Step4: Copy index file from AWS client to s3

aws s3 cp <LocalPath> <S3Uri> or <S3Uri> <LocalPath> or <S3Uri> <S3Uri>

aws s3 cp /root/index.html s3://xfusion-web-14165

# Step5: Enable static website hosting

Open bucket > Properties > Static website hosting > Edit

Enable: Static website hosting
Hosting type: Host a static website

Index document: index.html

Save

# Step6: Access the website

1. Open static website hosting endpoints in browser.

OR 

2. Open object and click on object URL
