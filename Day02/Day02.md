# Day 2: Create Security Group

# Step1: Login into AWS Console with the given credentials

# Step2: Create Security Group
Search for 'EC2' and open EC2 dashbaord > Secuirty Group > Create 'Security Group'

#create SG with the given values in task, also update 'Inbound Rules' as mentioned in the task

# Step3: Go back to terminal and run the below command to verify
$ aws ec2 describe-security-groups

#expected outpu

{
  "SecurityGroups": [
    {
      "Description": "default VPC security group",
      "GroupName": "default",
      "IpPermissions": [
        {
          "FromPort": 22,
          "ToPort": 22,
          "IpProtocol": "tcp",
          "IpRanges": [
            {
              "CidrIp": "0.0.0.0/0",
              "Description": "SSH access"
            }
          ],
          "Ipv6Ranges": [],
          "PrefixListIds": [],
          "UserIdGroupPairs": []
        }
      ],
      "IpPermissionsEgress": [
        {
          "IpProtocol": "-1",
          "IpRanges": [
            {
              "CidrIp": "0.0.0.0/0"
            }
          ],
          "Ipv6Ranges": [],
          "PrefixListIds": [],
          "UserIdGroupPairs": []
        }
      ],
      "OwnerId": "123456789012",
      "GroupId": "sg-0abc1234def567890",
      "VpcId": "vpc-0123abcd4567efgh"
    }
  ]
}

