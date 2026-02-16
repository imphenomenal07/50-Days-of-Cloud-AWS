# Day 15: Create Volume Snapshot

# # We are completing this via CLI

# Step1: Find the volume ID

aws ec2 describe-volumes --filters "Name=tag:Name,Values=devops-vol"  | grep "VolumeId"

# Step2: Create volume snapshot for the given volume

aws ec2 create-snapshot \
  --volume-id vol-077f060313cb33944 \
  --description "devops Snapshot" \
  --tag-specifications 'ResourceType=snapshot,Tags=[{Key=Name,Value=devops-vol-ss}]'

# Expected Output:

{
    "Tags": [
        {
            "Key": "Name",
            "Value": "devops-vol-ss"
        }
    ],
    "SnapshotId": "snap-0d56277548f636f75",
    "VolumeId": "vol-077f060313cb33944",
    "State": "pending",
    "StartTime": "2026-02-16T07:04:53.194Z",
    "Progress": "",
    "OwnerId": "045946725843",
    "Description": "devops Snapshot",
    "VolumeSize": 5,
    "Encrypted": false
}

# Step3: Verify the snapshot

aws ec2 describe-snapshots --snapshot-ids snap-0d56277548f636f75

# Expected Output:

{
    "Snapshots": [
        {
            "Tags": [
                {
                    "Key": "Name",
                    "Value": "devops-vol-ss"
                }
            ],
            "StorageTier": "standard",
            "TransferType": "standard",
            "CompletionTime": "2026-02-16T07:05:35.074Z",
            "FullSnapshotSizeInBytes": 0,
            "SnapshotId": "snap-0d56277548f636f75",
            "VolumeId": "vol-077f060313cb33944",
            "State": "completed",
            "StartTime": "2026-02-16T07:04:53.194Z",
            "Progress": "100%",
            "OwnerId": "045946725843",
            "Description": "devops Snapshot",
            "VolumeSize": 5,
            "Encrypted": false
        }
    ]
}
