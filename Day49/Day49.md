# Day 49: Centralized Audit Logging with VPC Peering

# Step1: Login into AWS Console

# Step2: Create required public vpc

AWS Console -> VPC -> Create VPC

Name:
CIDR: 10.0.0.0/16

# Step3: Create Public Subnet

VPC -> Subnets -> Create subnet

VPC: pub-vpc
Name:
CIDR:10.0.0.0/20
AZ: any

#After creation:
Enable Auto-assign public IPv4

# Step4: Internet Gateway

VPC -> Internet Gateways -> Create

Name:
Attach to devops-pub-vpc.

# Step5: Public Route Table

VPC -> Route Tables -> Create

Name: 
VPC: pub-vpc

Add route:

0.0.0.0/0 → Internet Gateway

Associate with devops-pub-subnet

# Step6: Create Public EC2

Create an EC2 instance with Public VPC and Public Subnet.
Use Ubuntu AMI and Same key pair that is used in Private EC2.
In SG, allow SSH, HTTP and HTTPS & create.

# Step7: Modify IAM role of Public EC2

Create IAM role with S3 Put Object permissions and All Resources and attach it to public EC2.

# Step8: Create a private s3 bucket

Block all public access while creating the bucket.

# Step9: Create VPC Peering connection

VPC -> Peering Connections -> Create

Name:
Requester: priv-vpc
Accepter: pub-vpc

Accept the peering request.

# Step10: Update both Route Tables 

#devops-priv-rt

Add route:
Destination: CIDR of pub-vpc
Target: peering connection

#devops-pub-rt

Add route:
Destination: CIDR of priv-vpc
Target: peering connection

# Step11: Setup SSH connections on AWS Client

$ cd .ssh
$ cp datacenter-key.pem id_rsa

#Login into Public EC2
$ssh -i /root/.ssh/datacenter-key.pem ubuntu@<PUBLIC_EC2_PUBLIC_IP>

exit

#Now, login into Private EC2 with same pem key
$ ssh ubuntu@<PRIVATE_EC2_PRIVATE_IP> -J ubuntu@<PUBLIC_EC2_PUBLIC_IP>

# Step12: Setup connection b/w Private & Public EC2

#On Priv EC2

$ ssh-keygen -t ed25519
$ cd .ssh/
$ cat id_ed25519.pub #Copy Content

#On Pub EC2

$ vi .ssh/authorized_keys #Paste the public key content that copied from Priv EC2

$ cd ~

$ mkdir boot

# Step13: Setup cron job on priv ec2

$ crontab -e
2

#Add this in cron file

* * * * * /usr/bin/scp /var/log/boots.log ubuntu@10.0.15.181:~/boot/boots.log

#make sure to update the given IP address with private IP of Pub EC2 instance.

# Step14: Setup cron job on pub ec2

$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o awscliv2.zip
$ sudo apt install -y unzip
$ unzip awscliv2.zip
$ sudo ./aws/install
$ aws --version

$ crontab -e
2

Add:
* * * * * aws s3 cp ~/boot/boots.log s3://datacenter-s3-logs-26648/datacenter-priv-vpc/boot/boots.log

#Make sure to update your private s3 bucket and boot log path.

# Step15: Final validation to verify task

Check and refresh your private s3 bucket. 'boots.log' will be there!!
