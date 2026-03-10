# Day 32: Snapshot and Restoration of an RDS Instance

# Step1: Login into AWS Console

# Step2: Go to Databases

AWS Console > Search 'RDS' > Open Dashboard > Databases

#Wait until DB instance becomes available

# Step3: Open AWS CLI agent and create snapshot

aws rds create-db-snapshot \
  --db-instance-identifier nautilus-rds \
  --db-snapshot-identifier nautilus-snapshot

# Step4: Restore snapshot

aws rds restore-db-instance-from-db-snapshot \
  --db-instance-identifier nautilus-snapshot-restore \
  --db-snapshot-identifier nautilus-snapshot \
  --db-instance-class db.t3.micro

# Step5: Verify the status of snapshot DB instance

aws rds describe-db-instances --db-instance-identifier nautilus-snapshot-restore | grep "DBInstanceStatus"

#Once it shows available, submit the task!!
