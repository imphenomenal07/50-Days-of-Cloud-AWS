# Day 28: Creating a Private ECR Repository

#We are completing this via CLI

# Step1: Create a private ECR

aws ecr create-repository \
    --repository-name datacenter-ecr \
    --region us-east-1

# Step2: Authenticate Docker to ECR

aws ecr get-login-password --region us-east-1 | \
docker login --username AWS --password-stdin 252520751240.dkr.ecr.us-east-1.amazonaws.com

# Step3: Build Docker image

#First go to the repo:

cd /root/pyapp

#Now create docker file:

docker build -t datacenter-ecr:latest .

# Step4: The the image for ECR

docker tag datacenter-ecr:latest \
252520751240.dkr.ecr.us-east-1.amazonaws.com/datacenter-ecr:latest

# Step5: Push Docker image to ECR

docker push 252520751240.dkr.ecr.us-east-1.amazonaws.com/datacenter-ecr:latest

# Step6: Now verify the image

aws ecr describe-images \
    --repository-name datacenter-ecr \
    --region us-east-1

# Expected Output:

{
    "imageDetails": [
        {
            "registryId": "252520751240",
            "repositoryName": "datacenter-ecr",
            "imageDigest": "sha256:f85ee6332592ac3fd30212824898e6586be0f229d763c93c3a8d741e3db65d13",
            "imageTags": [
                "latest"
            ],
            "imageSizeInBytes": 49724129,
            "imagePushedAt": 1772435201.02,
            "imageManifestMediaType": "application/vnd.docker.distribution.manifest.v2+json",
            "artifactMediaType": "application/vnd.docker.container.image.v1+json"
        }
    ]
}
