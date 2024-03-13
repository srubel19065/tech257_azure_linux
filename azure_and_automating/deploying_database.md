# Deploying a Database 
- [Deploying a Database](#deploying-a-database)
  - [Manually](#manually)
    - [Creating VM and installing MongoDB](#creating-vm-and-installing-mongodb)
    - [Changing the bindiP of mongoDB](#changing-the-bindip-of-mongodb)
    - [Configuring the connection between the app and database](#configuring-the-connection-between-the-app-and-database)
  - [Scripting](#scripting)


## Manually
### Creating VM and installing MongoDB
1. Create a VM for the database
2. Configurations:
   - name
   - SSH port only needed
   - private subnet
3. SSH into the VM
4. `sudo apt update -y` 
5. `sudo DEBIAN_FRONTEND=noninteractive apt-get upgrade -y
` - upgrade without user intervention needed
6. `curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc |    sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg    --dearmor
` - downloads mondoDB (database we will use)
7. ` echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list` - creates a list file
8. ` sudo apt-get update -y` - reupdate what has just been downloaded
9. `sudo apt-get install -y mongodb-org=7.0.6 mongodb-org-database=7.0.6 mongodb-org-server=7.0.6 mongodb-mongosh=2.1.5 mongodb-org-mongos=7.0.6 mongodb-org-tools=7.0.6
` - installs mongoDB 7.0.6 
10. `systemctl status mongod` - checks the system to see whether it has installed but will show that its not actively running

### Changing the bindiP of mongoDB
**This is because we need to be able to accept connections from anywhere so would need to set it as 0.0.0.0**
1. `sudo nano /etc/mongod.conf` - nano into the config file that has the bindiP
2. Change the iP to 0.0.0.0
3. `cat` - displays whether the change worked
4. ` sudo systemctl start mongod` - starts mongo
5. ` sudo systemctl enable mongod` - enables it so everytime it start will make it active
6. can check the status again to see whether it is active

### Configuring the connection between the app and database
**Azure by default allows internal connections and this is done through private iP address if two subnets are in the same VNet**
1. Open another gitbash and SSH into the app
2. We need to create a env variable which will establish the connection:
   1. `export DB_HOST=mongodb://<ip-address>:27017/posts` - this provides the private address of the database VM which will be used to communicate with each other
   2. `printenv DB_HOST` - print to check if it was correctly made
3. cd into your app folder
4. We need to stop pm2 from running so that node can be stopped in order for us to do an npm start:
    1. `ps aux` - to find ID of pm2
    2. `sudo kill ID`
 5. `sudo -E npm install` - installs node whilst as the root user and using the environment variable (-E)
 6. `sudo -E npm start` - will start the app 

**The app and database can now communicate and can be viewed by entering `public ip` followed by /posts**
![Alt text](image.png)

## Scripting 
Script to automate deployment of database:
```
#!/bin/bash

# update
sudo apt update -y

# This upgrade makes all upgrades noninteractive and dont need user input
sudo DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

# download mongoDB
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
   --dearmor

# creates a list file
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# reupdate
sudo apt-get update -y

# install mongoDB 
sudo apt-get install -y mongodb-org=7.0.6 mongodb-org-database=7.0.6 mongodb-org-server=7.0.6 mongodb-mongosh=2.1.5 mongodb-org-mongos=7.0.6 mongodb-org-tools=7.0.6
 
# will change the bindip to 0.0.0.0
sudo sed -i 's@127.0.0.1@0.0.0.0@' /etc/mongod.conf

# start and enable mongoDB
sudo systemctl start mongod
sudo systemctl enable mongod
```