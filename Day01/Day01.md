# Day 1: Create Key Pair

# Step1: Login into AWS console with the given credentials
# Step2: Create key pair
#Search and open EC2 Dashboard > Key pair > create key-pair

# Step3: Run below command in terminal to verify
$ aws ec2 describe-key-pairs

#Expected Output

{
  "KeyPairs": [
    {
      "KeyName": "my-key-pair",
      "KeyPairId": "key-0abc1234def567890",
      "KeyType": "rsa",
      "Tags": [],
      "PublicKey": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC7...",
      "CreateTime": "2024-06-15T10:42:31.000Z"
    }
  ]
}

