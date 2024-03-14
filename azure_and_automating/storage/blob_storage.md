# Blob Storage

## What is it?
Blob storage is a type of storage in Azure that allows the storing of objects and unstrucutred data
- **BLOB = Binary Large Object** 
  - large amount of data in binary form that dont have any particular file format
  - Blob storage keeps these data in storage areas called Data Lakes
  - blobs are stored in containers


## Creating Blob Storage 

### 1. Log into AZ
1. `az login` - This will give a link and a code to enter into the link and it should log you in
### 2. Create Storage account
1. `az storage account create --name tech257rubelstorage --resource-group tech257 --location uksouth --sku Standard_LRS` - Creates a storage account with resource group, location and type of storage
2. `az storage account list --resource-group tech257 ` - lists the storage accounts within the resource group (but gives in json format and looks very messy and unreadable)
3. `az storage account list --resource-group tech257 --query "[].{Name:name, Location:location, Kind:kind}" --output table` - Lists the storage accounts but formats it within a table and can give specifically want to want to see outputted

### 3. Create Container
1. `az storage container create \
    --account-name tech257rubelstorage \
    --name testcontainer` - creates a container within the storage account given but gives a warning after
    - *cant find credentials* - we havent given any credentials to authorise this, it still works and creates however better to use credentials
2. `az storage container create \
    --account-name tech257rubelstorage \
    --name testcontainer \
	--auth-mode login` - This creates the container using a auth mode command that gives permission and no longer has any problems
3. `az storage container delete \
    --account-name <storageAccount> \
    --name <container> \
    --auth-mode login` - deletes the container

### 4. Uploading blob to the container
1. `az storage blob upload \
    --account-name <storageAccount> \
    --container-name testcontainer \
    --name <name that is seen on the GUI> \
    --file <fileName> \
    --auth-mode login`
2. `az storage blob list \
    --account-name tech257rubelstorage \
    --container-name testcontainer \
    --output table \
    --auth-mode login` - lists the blobs 

### 5. Given Public access to the blob
**This is because by default it is private and account be accesses publicly**
1. Go to the Storage account on Azure
2. Settings, `Configuration` - enable `Allow Blob anonymous access`
3. If you go to Containers, then to the file and try checking the URL, it pops up with 'this does not exist', this is for security reasons 
4. In the Container `Change access level` to blob(anonymous read access)
5. This will allow public viewing

## Blob Image on the APP
### Manually 
1. `az storage account create --name tech257rubelstorage --resource-group tech257 --location uksouth --sku Standard_LRS` - creates storage account
2. `az storage account update \
    --name tech257rubelstorage \
    --resource-group tech257 \
    --allow-blob-public-access true` - # allows blob public access
3. `az storage container create \
    --account-name tech257rubelstorage \
    --name spartacontainer \
	--auth-mode login` - creates container
4. `sudo curl -o sunset.png https://pixabay.com/get/gaec9d642cb58dbccf6bed93d60b6d47886c4499630c57e16e9e0f8fc53622b7b8f5f69a80b8996057235c2175b4bf0429ae23529cd506a375479f7790ef8b4e9_1280.jpg` - using curl but as root user to download the image
5. `az storage blob upload \
    --account-name tech257rubelstorage \
    --container-name spartacontainer \
    --name sunset.png\
    --file sunset.png \
    --auth-mode login`