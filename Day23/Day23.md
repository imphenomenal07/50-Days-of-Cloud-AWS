# Day 23: Data Migration Between S3 Buckets Using AWS CLI

# Step1: Create a new bucket

aws s3 mb s3://devops-sync-13505

#Buckets created via CLI, all are private by default!!

# Step2: Verify the bucket ownership and privacy

aws s3api get-public-access-block --bucket devops-sync-13505

# Step3: Migrate data one bucket to another bucket

#Cmd format: aws s3 sync s3://source-bucket s3://dest-bucket

aws s3 sync s3://devops-s3-27026 s3://devops-sync-13505

# step4: Now verify the data of both buckets

aws s3 ls s3://devops-s3-27026

aws s3 ls s3://devops-sync-13505

Data available in both bucket will be same!!
