# Day 31: Configuring a Private RDS Instance for Application Development

# Step1: Login into AWS Console

# Step2: Go to Databases

AWS Console > Search 'RDS' > Open Dashboard > Databases

# Step3: Create Database

Choose a database creation method: Full configuration
Engine options: MySQL
Engine Version: 8.4.X
Templates: Free tier

Setting: DB cluster identifier -> Name of DB
         ✅Auto generate password

Instance type: db.t3.micro

Storage  type: General Purpose SSD (gp3)

✅Enable auto scaling
Maximum storage threshold: 50

Leave rest of the things as default.

And 'Create Database'

# Wait for 4-5 mins until DB comes active!!
