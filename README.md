# Task3: 
## How to identify the issue of too many open files and solve it.

The Too many open files message occurs on UNIX and Linux operating systems. The default setting for the maximum number of open files might be too low.  
1. To get the maximum number of file descriptors your system  
   ```sh 
   cat /proc/sys/fs/file-max
   ```
1. To check the open file limit for a current user 
    ```sh 
    ulimit -n 
    ```
1. To list opened files by a specific user 
    ```sh 
    lsof -u <user>
    ```
1. To lists all open files belonging to specific PID (process ID)
    ```sh 
    lsof -p <process_ID>
    ```
There are two limit types: Hard and Soft. A user can change a soft limit (however, the soft value cannot exceed the hard one). Only a privileged or root user can modify a hard limit value.    
 
1. To display the soft limit
   ```sh
   ulimit -nS
   ```
   
1. To display the hard limit value
   ```sh 
   ulimit -nH
   ```
 To allow all services open a large number of files, you can change the limits in your Linux OS. Update `/etc/security/limits.conf` to make changes permanent. 
 ```sh 
  * hard nofile 97816
  * soft nofile 97816
 ```
1. Reload the terminal after chaning  `/etc/security/limits.conf`
   ```sh 
   ulimit -n
   ```
 

# Task4 
## Disk space is 100% utilized on server and most used by /usr/src

1. To see whats taking up the most space in a the server and on usr. 
   ```sh 
   du -a / | sort -n -r | head -n 20
   du -a /usr | sort -n -r | head -n 20
   ```

1. mostly /usr/src containes packages and libraries which are installed. so we can cleanup unused packages or libraries with below command. 
   ```sh 
   package-cleanup --leaves --all
   ```

1. For other filesystems or directories we can enable logrotate in the cronjob so that it get archive or cleanup automatically. For this we can install logrotate (`yum install logrotate`) or can write a shellscript 

