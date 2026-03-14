# Day 35: Deploying and Managing Applications on AWS

# Step1: Login into AWS Console

# Step2: Go to Databases

AWS Console > Search 'RDS' > Open Dashboard > Databases

# Step3: Create Database

Choose a database creation method: Full configuration
Engine options: MySQL
Engine Version: 8.4.5
Templates: Free tier

# Setting:

DB cluster identifier -> Name of DB

Master username:

Password: admin123

Instance type: db.t3.micro

Storage  type: General Purpose SSD (gp2)
Allocated Storage: 5 GiB

# Additional Configuration:
Initial database name: name-of-database

Leave rest of the things as default.

And 'Create Database'

#Wait for 4-5 mins until DB comes active!!

# Step4: Update 'inbound rules' of SG for the existing instance

Add: SSH
     HTTP
     HTTPS
     MySQL/Aurora

Allow 'Anywhere from IPv4' and Save!

# Step5: Connect to EC2 with via cloud shell with 'root' user

# Step6: Configure passwordless authentication for the EC2

Create RSA key on AWS client

$ ssh-keygen -t rsa

$ cd .ssh

$ cat rsa.id_pub  #Copy content and paste on cloud shell at below location

$ cd .ssh #on cloud shell

$ vi authorized_keys #Paste content in the file, then save and exit

# Step7: Go to AWS Client and access the instance

$ ssh root@pub-ip-of-ec2  #Exit from the ec2, if logged in successfully!!

# Step8: Copy 'index.php' file to ec2 at location '/var/www/html'

$ scp index.php root@pub-ip-of-ec2:~

$ ssh root@pub-ip-of-ec2

$ mv index.php /var/www/html

# Step9: Update 'index.html' file

$ cd /var/www/html

#Remove 'index.html' file, if available!!

$ vi index.php

<?php
$dbname = 'devops_db';
$dbuser = 'devops_admin';
$dbpass = 'admin123';
$dbhost = 'devops-rds.cpkaycwa4j4x.us-east-1.rds.amazonaws.com';

$link = mysqli_connect($dbhost, $dbuser, $dbpass) or die("Unable to Connect to '$dbhost'");
mysqli_select_db($link, $dbname) or die("Could not open the db '$dbname'");

$test_query = "SHOW TABLES FROM $dbname";
$result = mysqli_query($link, $test_query);

$tblCnt = 0;
while($tbl = mysqli_fetch_array($result)) {
  $tblCnt++;
}

if (!$tblCnt) {
  echo "Connected successfully<br />\n";
} else {
  echo "Connected successfully<br />\n";
}
?>

#Save and exit from vi editor!!

# Step10: Check connection

$ curl localhost

#Expected Output:

Connected successfully
