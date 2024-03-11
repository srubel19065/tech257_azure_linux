# Deploying app to VM

- [Deploying app to VM](#deploying-app-to-vm)
  - [Create new VM](#create-new-vm)
    - [Copying App Folder into VM](#copying-app-folder-into-vm)
    - [Using Github](#using-github)
    - [Script for Deploying the app](#script-for-deploying-the-app)
    - [Reverse Proxy](#reverse-proxy)


## Create new VM
Follow steps to create new VM but new config:
1. `Image` - new image change to Ubuntu 22.04 (latest version)
2. `VNet` - Create new one (will be used everytime as new default)
    1. Set address range
    2. As we will use two subnets (public and private), add two with two address ranges
3. `NIC NSG` - As we will be accessing the app through a different port, a new one will need to be created
    1. `Advanced` - custom NSG settings
    2. `create new`
    3. `Add inbound rule` - Select Custom and input port 3000 (will be the port used to enter)
 4. Add tags
 5. SSH into the vm (same method as usual)



### Copying App Folder into VM
1. `scp` = way to copy something locally into a vm
   - scp -i ~/.ssh/privateKey -r ~/Downloads/app adminuser@172.167.179.17:.

### Using Github
1. Create  git repo, move the app folder to that repo
2. Git Clone in the script


### Script for Deploying the app

```
#!/bin/bash

# update and upgrade
sudo apt update -y
sudo apt upgrade -y

# install nginx
sudo apt install nginx -y

# enable nginx and be able to restart everytime
sudo systemctl restart nginx
sudo systemctl enable nginx

# download node.js
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - &&\

# installl node.js
sudo apt-get install -y nodejs

# Retrieving the app folder from the git repo
git clone https://github.com/srubel19065/tech257_sparta_app.git

# getting into the app folder
cd tech257_sparta_app/app/

# installing npm
npm install

# installing pm2 
sudo npm install pm2@latest -g

# start pm2 but restart everytime its deployed 
pm2 restart app.js
```

### Reverse Proxy