# Day 38: Deploying Containerized Applications with Amazon ECS

# Step1: Login into AWS Console

# Step2: Update the default Security Group with Port 80

AWS Console > EC2 > Security Groups > Click on Security Group > Edit Inbound rule > Add 'HTTP' - Anywhere from IPv4 > Save

# Step3: Create Private Elastic Container Registry

AWS Console > ECR > Repositories > Create private repository

Repository name:

Turn on 'Scan on push'

Create

# Step4: Create Docker image and push to ECR

#Go to working dir
cd pyapp

#Login into ECR repo on AWS client
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 717790468997.dkr.ecr.us-east-1.amazonaws.com

#Build docker image
docker build -t nautilus-ecr .

#Tag the image
docker tag nautilus-ecr:latest 717790468997.dkr.ecr.us-east-1.amazonaws.com/nautilus-ecr:latest

#Push image to ECR
docker push 717790468997.dkr.ecr.us-east-1.amazonaws.com/nautilus-ecr:latest

# Step5: Create Cluster

AWS Console > ECS > Clusters > Create cluster

Cluster name:

Infrastructure: Fargate only

Create

# Step6: Create Task definitions

AWS Console > ECS > Task definitions > Create new task definitions

Task definition family name:

Launch Type: AWS Fargate

Container name: 

Image URI: Browse ECR images

           Choose a repo

Create

# Step7: Create service

Once task definition is created, click on it to open and create

Task Definition > Deploy > Create Service

# Step8: Verify deployment

Amazon Elastic Container Service > Clusters > nautilus-cluster > Tasks > Task-id '0dd66d034e664955a222ce16dcca6ed8' > Configuration > Open 'IPv4 Public IP'
