# Day 50: Expanding EC2 Instance Storage for Development Needs

# Step1: Login into AWS Console

# Step2: Modify the EC2 volume

Console -> EC2 Dashboard -> Instances -> Open require EC2 instance -> Storage -> Open Volume ID -> Select 'VolumeID' -> Actions -> Modify Volume

#Increase volume size and Modify

# Step3: Login into EC2

$ ssh -i pem-key ec2-user@ec2-pub-ip

# Step4: Update Volume

$ lsblk
$ sudo growpart /dev/xvda 1
$ sudo xfs_growfs /

# Step4: Final step to verify

$ df -h
