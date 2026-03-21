# Day 41: Securing Data with AWS KMS

# Step1: Login into AWS Console

# Step2: Create KMS Key

AWS Console > Search for 'KMS' & open > Create key

Key type: Symmetric
Key usage: Encrypt and decrypt

Next

Alias: name of kms key

Next

Key administrator: your-lab-user

Next

Key users: your-lab-user & select others as per requirement

Next

Key Policy: Go with default

Then review & Finish

# Step3: Enable KMS key

Select the Key > Actions > Enable

# Step4: Encrypt file available at /root location on AWS Client

aws kms encrypt \
  --key-id 405fe2e1-90be-4007-bb66-44c194327f90 \
  --plaintext fileb:///root/SensitiveData.txt \
  --output text \
  --query CiphertextBlob | base64 \
  --decode > EncryptedData.bin

# Step5: Verify data integrity

aws kms decrypt \
    --ciphertext-blob fileb://EncryptedData.bin \
    --key-id 405fe2e1-90be-4007-bb66-44c194327f90 \
    --output text \
    --query Plaintext | base64 \
    --decode > PlaintextFile.txt

# Step6: Compare both files

diff /root/SensitiveData.txt /root/PlaintextFile.txt

#Expected output:

No output → files are identical
