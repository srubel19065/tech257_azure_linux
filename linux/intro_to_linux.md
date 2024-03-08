# Linux

- [Linux](#linux)
  - [What is it](#what-is-it)
  - [Commands](#commands)
  - [Scripting](#scripting)
    - [Example: Provisioning NginX Script](#example-provisioning-nginx-script)
  - [Variables](#variables)
    - [Env Variables](#env-variables)
    - [Making the env variable persistant](#making-the-env-variable-persistant)

## What is it
- Operating System
- On Windows, its a tiny piece that interprets commands
- Bash = *Bourne Again Shell*


## Commands
- `ls`
  - whats inside 
- `ls -a`
  - hidden files
- `pwd`
  - Present working directory
- `cat /etc/shells`
- `ps -p $$`
- `cd` 
  - takes back to home
- `ls -la`
  - shows info for each including hidden file/directory
- `ls -l`
  - shows info of file/directory
- `file <filename`
  - shows type of file
- `curl` 
  - can download files 
- `cp`
  - copies a file
- `mv`
  - either move file or rename
- `mkdir`
  - make directory
- `rm`
  - remove a file
    - `-r` = recursively delete
    - `-d` = empty directory
- `touch` 
  - empty file
- `nano <file>`
  - file editor 


## Scripting 
Can create a script using the Nano editor command

### Example: Provisioning NginX Script
- This is a script - helps to automate tasks.
- Create a file and use Nano to edit the file.

```
#!/bin/bash

# update
sudo apt update -y

# upgrade
# issue - current command asked for user input
sudo apt upgrade -y

# install nginx
sudo apt install nginx -y

# restart nginx
sudo systemctl restart nginx

# enable nginx
sudo systemctl enable nginx
```
- To execute, use `chmod +x` to add execute permissions and then run the script using `./` in front of script name

## Variables
### Env Variables 
Variables stored by the Operating System in memory
- `printenv` = prints all env variables on the system
- `printenv USER` = prints user name
 1. Variables = `MYNAME=rubel` - this is just a variable, assigned a value to something but isnt an env
 2. To make env use `export ENVNAME=...` 
   - This export term makes the variable env

### Making the env variable persistant
1.  When you make an env, if they arent persistant then they will be lost every time the VM is closed
2.  Go to the .bashrc file - purpose is to be read by bash and interact with it thats why env are stored here
3.  `nano .bashrc` = scroll to bottom and create your env
4.  exit and soruce(reload)
5.  env should become persistant
