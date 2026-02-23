# Day 22: Configuring Secure SSH Access to an EC2 Instance

# Step1: Create SSH keys on terminal
$ ssh-keygen -t rsa

# Step2: Login into AWS console
Now create an EC2 instance without key-pair login!!

# Step3: Connect to Cloud shell
Once instance is created and running, then select the instance and click on 'Connect' button.

# Step4: Change to root or super user
$ sudo su

# Step5: Secure SSH file authentication

#On Kodekloud terminal

$ cd .ssh
$ cat id_rsa.pub  #Copy the content


#Go back to Cloud shell terminal and keep the content at correct location

$ cd /root/.ssh
$ vi authorized_keys  #Paste content in the file, save and exit

# Step6: Go back to Kodekloud terminal and login into the instance
$ ssh root@ec2-instance-public-ip
