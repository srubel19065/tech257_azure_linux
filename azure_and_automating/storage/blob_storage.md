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