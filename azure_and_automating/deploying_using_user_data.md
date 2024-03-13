# User Data & Image

Automating using user data is the next level up from scripting. It allows the process to be quicker as we dont need to use SSH to log in, rather once the VM is created, the public iP will load the app

## How to deploy using User Data
1. Make sure the bash script is working
2. Create a new VM but at the `advanced` config, paste the script into the `user data` field
3. After creation paste the iP into browser and wait for the process (should take a few minutes)

## How to deploy using Image and bit of User Data
1. 


## Updated Script
   1. `sudo DEBIAN_FRONTEND=noninteractive apt-get upgrade -y` - This command makes sure all upgrades including kernel are done without user intervention
   2. `cd /` - cd into the root folder before cloning
```
#!/bin/bash

# update and upgrade
sudo apt update -y
# sudo apt upgrade -y

# This upgrade makes all upgrades noninteractive and dont need user input
sudo DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

# install nginx
sudo apt install nginx -y

# enable nginx and be able to restart everytime
sudo systemctl restart nginx
sudo systemctl enable nginx

# download node.js
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - &&\

# installl node.js
sudo apt-get install -y nodejs

# going to root user
cd /

# Retrieving the app folder from the git repo
git clone https://github.com/srubel19065/tech257_sparta_app.git

# getting into the app folder
cd tech257_sparta_app/app/

# installing npm
npm install

# installing pm2 
sudo npm install pm2@latest -g

# stop pm2 before rerunning
pm2 stop app.js

# start pm2 
pm2 start app.js
```