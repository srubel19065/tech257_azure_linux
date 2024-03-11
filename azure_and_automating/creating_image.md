# Images

Images are snapshot operating systems used on VMs for example Ubuntu.

## Creating an Image
You will need AZ CLI for the first part so make sure to download and install, then to check do `az 
--version`

1. On GitBash, in the current running VM, make sure everything is backed up and not needed as everything not in root will be wiped
2. `sudo waagent -deprovision+user` - will wipe everything to root level
3. exit the VM
4. log into az with `az login`
5. `az vm deallocate --resource-group <yourResourceGroup> --name <yourVMName>` - will stop the VM
6. `az vm generalize --resource-group <yourResourceGroup> --name <yourVMName>` - take generalised configurations and apply it
7. Go back to azure to the VM, next to Hibernate click `Capture` - this will create an image
![Alt text](image.png)
8. We only want to capture managed image and below make the name appropriate
### Creating a VM with Own image
1. `Create VM` - from the image page should take you to creating a VM with that new image selected automatically
2. Choose a name, make sure new Image is selected and all standard settins configured
![Alt text](image.png)
1. Select  `Other` for license type
2. All other config should be same