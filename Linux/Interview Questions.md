## 1.Explain the basic features of the Linux OS.

Some basic features of Linux are:

Linux is free and easily available.
It is more secure than other operating systems because it uses security auditing and password authentication features.
Linux has its personal software repository.
It includes multiple languages throughout the world. Hence Linux supports different language keyboards.
It offers CLI and GUI to use different commands and applications such as Firefox, VLC, etc.

## 2.Name some Linux Distros

There are various Linux distros but the following are the most commonly used:
Ubuntu
Debian
CentOS
Fedora
RedHat

## 3.Define the basic components of Linux.

Majorly there are five basic components of Linux:

**Kernel:** Linux kernel is a core part of the operating system that works as a bridge between hardware and software.
**Shell: ** Shell is an interface between a kernel and a user.
**GUI: ** Offers different way to interact with the system, known as the graphical user interface (GUI).
** Application programs:** It is designed to perform a bundle of tasks through a bundle of functions.
** System Utilities:** It is the software functions through which users manage the system.

## 4. File Permissions in Linux ##

** Read:** Users open and read files with this permission.
** Write:** Users can open and modify the files.
** Execute:** Users can run the file.

## 5. What is a root account? ##

The root is like the user's name or system administrator account in Linux. The root account provides complete system control, which an ordinary user cannot do.

## 6. Describe CLI and GUI in Linux. ##

CLI, i.e., command line interface. It takes input as a command and runs the tasks of the system. The term GUI refers to the Graphical User Interface or the human-computer interface. It uses icons, images, menus, and windows, which can be manipulated through the mouse.

## 7. What is the difference between hard links and soft links? ##

** Hard Links: ** 
It includes original content.
Hard links are faster as compared to soft links.
There is no relative path for hard links.
It uses less memory.
Any change in this link reflects other files directly.

** Soft Links: **
It includes the original file location.
Soft links are slower.
Relative paths are used for soft links.
It uses more memory.
Every change in this link reflects its hard link and the actual file directly.

## 8. How do you troubleshoot network connectivity issues in Linux? ##

There are multiple ways to troubleshoot the network connectivity and find the issue correctly:

**Check the Internet Connectivity:**

First of all, please check if the internet connection option is on and also check the cables to find if there is any issue with it.

**Verify the Network Configuration:**

Please check that your network is configured correctly and the network interface has your IP address. You can check it by running the ip addr or ifconfig commands.
You can also run the ip route command to check if the default gateway is set properly.
Finally, verify the DNS server configuration in the /etc/resolv.conf file.

**Check the Firewall:**

Sometimes, firewall rules block the internet connection for the system's security. Hence, you can run the ufw or iptables command to modify the firewall rules.

**Network Interface:**

You can restart your network interface through the ifup and ifdown commands. Once you restart the network interface, please reboot the system to make changes successful.

## How do you list all the processes running in Linux?

You can list the currently running process in Linux through various commands such as:

**ps Command:**

The ps command displays brief information about the running processes. You can use the ps -f or ps -f command because the -f option shows the full-format result, and the -e option displays all processes. Moreover, you can use the ps auxf command to get a detailed list of processes.

**top and htop Command:**

The top command displays the real-time details about the system process and the complete resource usage.
The htop command is the improved version of the top command because it displays the color-coded list with additional features such as sorting, filtering, sorting, etc.

## What is the chmod command in Linux, and how do you use it?

You can use the chmod command to change the file permissions of the directories. It offers a simple way to control the read and write permissions. For instance, if you want to change the permission of the ABC.sh script and give it the write and executable permission, you can run the below command:

*chmod u+wx ABC.sh*
The chmod command is not limited to the write (w), read (r), and executable (x) permissions because there are symbolic modes.

## 9.How do you check disk space usage?

There are some simple commands you can use to check disk space usage, such as:

** df Command: **

The df or disk-free command shows the used and the available disk space. You can use the additional options to check disk space differently. For instance, you can use the df -h command to check the disk usage in the human-readable format.

** du Command: **

The du or disk usage command estimates and shows the disk space usage, so running the du command with no option shows the disk usage of your current directory. However, you can run the following command to check the disk usage of a specific directory:

*du -sh ~/<directory>*

## 10.What is the rsync command, and how do you use this command for synchronization?

The rsync command is used to synchronize and transfer the files in Linux. It synchronizes files between two local systems, directories, or a network. The basic rsync command contains the following:

*rsync <options> <source> <destination>*
For example, let's synchronize between Documents and the Downloads directory. For this, you need to run the following command:

*rsync -av ~/Documents ~/Downloads*

## 11.How do you secure a Linux server?
There are multiple methods to secure the Linux server and protect it from data breaches, security threats, and unauthorized access. Here are some of these methods:

*Create a strong password
Update the server and apply security patches.
Use secured protocols like SSH and configure it to use key-based authentication for higher security.
Use the intrusion detection system (IDS) to monitor network traffic and prevent malicious activities.
Configure the firewall to limit the inbound and outbound traffic on the server.
Disable all unused network services.
Create regular backups.
Review logs and perform regular security audits.
Encrypt network traffic and enable monitoring.*

## 12.What are the most important Linux commands?
There are a ton of useful commands in Linux, and here are some of the commonly used commands:

ls: Display directory contents such as folders and files.
mkdir: Used to create a new directory.
pwd: Shows the current directory.
top: Display system running processes and resource usage.
grep: Search a specific pattern in a file.
cat: Through this command, users can add multiple files and also display the content of the files.
tar: Archives directories and files into a tarball.
wget: Download files from the browser or web.
free: Shows memory usage.
df: Shows disk space usage.
man: Gives a manual page for a specific command that displays instructions and details.

## 13.What is the difference between absolute and relative paths in Linux?

Absolute path = It specifies the exact location of a file or directory from the root directory ("/"). We will notice that they always start with a forward slash ("/").

For Example: `/home/user/jayesh/geeksforgeeks.txt`

Relative paths = It specifies the location relative to the current working directory. In this we do not start with a forward slash ("/").

For Example: `documents/file.txt`

## 14. What is the grep command used for in Linux?

The grep command is used to search for specific patterns within files or input streams. It allows us to find and print lines that we give to match the pattern.

For example: If we want to search `test` in a text file name "file.txt". We use the following command

grep "test" file.txt
This command will search for the word `test` in the file named "file.txt" and print the matching lines.

## 15. How do you find and replace text in a file using the sed command in Linux?

The sed command (stream editor) can be used to find and replace text in a file. The basic syntax is sed 's/pattern/replacement/g' filename.

For example: to replace all occurrences of "true" with "False" in a file

sed 's/true/False/g' file_name

## 16.How do you start and stop a service in Linux?
The 'systemctl start <service>' command is used to start a service, and 'systemctl stop <service>' is used to stop a service in Linux.

## 17. What are common causes of file permission issues in Linux?
Common causes of file permission issues in Linux include incorrect ownership, improper permissions set for users or groups, and conflicts between different users' permissions.

## 18. How do you check the system logs in Linux?
System logs can be checked using the 'tail' or 'less' command to view the contents of log files located in the '/var/log' directory, such as 'syslog', 'messages', or 'auth.log'.

## 19. How would you troubleshoot a slow-performing Linux server?
Troubleshooting steps might involve checking system resource usage with tools like 'top' or 'htop', monitoring disk I/O, analyzing network traffic, identifying memory or CPU bottlenecks, and reviewing application logs.
