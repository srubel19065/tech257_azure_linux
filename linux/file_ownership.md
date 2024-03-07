# File Ownership

## Task 2.8a: Linux - Research managing file ownership
### 1. Why is managing file ownership important?
1. Security:
   - Access Control - type of ownership shows who can access and modify. Appropriate ownership prevents unauthorised access, data breaches and modifications that were accidental. Also allows each individual to be given only what they need
   - System Integrity - specific system files should only be accessed by specific users
2. Accountability:
   - Identifying Users - we can see who did what 
3. Collaboration:
   - Shared access - when collaborating, everyone has correct permissions according to what they need
4. Organisation & Efficiency:
   - Resource management - identify unused or old files with users who dont need them 
   - Project management - helps organise project by knowing who is in charge of each

### 2. What is command to view file ownership
`ls -l`
- Gives info on each file including the permissions
- Can be specific by giving filename after

### 3. What permissions are set when a user creates a file or directory? Who does file or directory belong to?
- Owner: Read, Write, and Execute (rw) --> The creator gains ownership
- Group: Read and Execute (r)
- Others: None 

### 4. Why does the owner, by default, not receive X permissions when they create a file?
Having full control increases security risk, some things could be executed by mistake when not intended, principle is least privilege

### 5. What command is used to change the owner of a file or directory?
`chown <new owner> <filename>`
- `chown` = change owner

## Task 2.8b: Linux - Research managing file permissions
### 1. Does being the owner of a file mean you have full permissions on that file? Explain.
It does not mean you are given full permissions, will have read and write but will need to be granted execute. This is because just for owning a file, having full control would pose security risks.

### 2. If you give permissions to the User entity, what does this mean?
The user is the owner of the file/directory. They have the most permissions and get full control except execute by default. 

### 3. If you give permissions to the Group entity, what does this mean?
Members of a group are given permissions with that group being assigned the permissions, so whoever is added to that group gets those permissions. 

### 4. If you give permissions to the Other entity, what does this mean?
Other refers to those who are not the owner, not part of a specified group and they are given the least amont of permissions

### 5. You give the following permissions to a [file: Use](file: Us "‌")r permissions are read-only, Group permissions are read and write, Other permissions are read, write and execute. You are logged in as the user which is owner of the file. What permissions will you have on this file? Explain.
As the User, you can only read

### 6. Here is one line from the ls -l. Work out everything you can about permissions on this file or directory.

-rwxr-xr-- 1 tcboony staff  123 Nov 25 18:36 keeprunning.sh

- `-rwx` = Owner/User can read, write, execute
- `r-x` = Group can read and execute
- `r--` = Other can only read

## Task 2.8c: Linux - Research managing file permissions using numeric values
### 1. What numeric values are assigned to each permission?
Read = 4
Write = 2
Execute = 1

### What can you with the values assign read + write permissions?
6

### What value would assign read, write and execute permissions?
7

### What value would assign read and execute permissions?
5

### Often, a file or directory's mode/permissions are represented by 3 numbers. What do you think 644 would mean?
Each number represents the permissions assigned to each entity
- 6 = Read and Write --> User
- 4 = Read --> Group
- 4 = Read --> Other

## Task 2.8d: Linux - Research changing file permissions
### 1. What command changes file permissions?
chmod

### 2. To change permissions on a file what must the end user be? (2 answers)
The owner of that file and have the Write permission

### 3. Give examples of some different ways/syntaxes to set permissions on a new file (named testfile.txt) to:
a. 