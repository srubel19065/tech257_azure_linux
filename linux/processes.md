# Processes

## What is a Process
- A program running in memory 
- PID: Process ID
- TTY: Terminal session code

## Process Commands

- ```ps``` = Gives user processes in snapshot form of that exact moment
- ```ps -e``` = Gives basic list of all processes
- ```ps aux``` = Gives more in depth list of processes including CPU, Memory, Start time etc
- ```top``` = Shows list of processes whilst they are running instead of snapshot 
  - ```shift m``` = memory order
  - ```shift n``` = PID order
  - ```shift p``` = Processor order
- ```jobs``` = shows which jobs currently running 

## Making Process
Can create a process for example Sleep process: will make the terminal sleep for amount of time specified
- ```sleep <time(s)>``` = sleep incuding terminal
- ```sleep <time(s)> &``` = & - does in the background
- After making a process, it will output its PID but can also be seen when `ps aux` 

## Terminating Vs Killing
Processes can be made to shut down but type of command will do the level of it
- `Kill` = will terminate process at mild level
- `Kill -9` = will kill process with brute force
  - can lead to creating zombie processes 
  - A Zombie process can be created if you terminate a parent process whilst it has child processes running
    - This is because the child process will have nothing to manage it therefore will still be there and can cause issues