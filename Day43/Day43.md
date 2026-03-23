# Day 43: Scaling and Managing Kubernetes Clusters with Amazon EKS

# Step1: Login into AWS Console

# Step2: Verify the IAM role. If not available, then create one with the same name as given in task

# Step3: Create EKS Cluster

AWS Console > Search 'EKS' > Create Cluster

Configuration options: Custom configuration

EKS Auto Mode: Disable it

Name:
Cluster IAM role:

Next

VPC: Default
Subnets: zone -a, zone - b and zone - c

Security group: default

Cluster endpoint access: Private

Next 

Select 'Configure Observability', 'Select add-ons' and 'Configure selected add-ons settings' as per your requirement or leave them as default

Create

# Step4: Wait until cluster comes in ACTIVE state!!
