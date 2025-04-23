

---

### **Basic Commands**



1. **`pwd`** - Print the current working directory.
   - Example: `pwd`

2. **`ls`** - List files and directories in the current directory.
   - Example: `ls -l` (long listing format)

3. **`cd`** - Change directory.
   - Example: `cd /home/user`

4. **`cp`** - Copy files and directories.
   - Example: `cp file1.txt /home/user/`

5. **`mv`** - Move or rename files and directories.
   - Example: `mv file1.txt newfile.txt`

6. **`rm`** - Remove files and directories.
   - Example: `rm -r /home/user/dir/` (delete directory)

7. **`mkdir`** - Create a new directory.
   - Example: `mkdir newdir`

8. **`rmdir`** - Remove an empty directory.
   - Example: `rmdir emptydir`

9. **`cat`** - Display file content.
   - Example: `cat file.txt`

10. **`touch`** - Create an empty file.
   - Example: `touch newfile.txt`

11. **`man`** - Display manual for a command.
   - Example: `man ls`

---

 ---

### 🔹 `sudo` – Run commands with superuser (root) privileges  
**Example:** `sudo apt update` – Update package lists as root.

---

### 🔹 `systemctl` – Manage and control system services  
**Example:** `sudo systemctl start tor` – Start the Tor service.

--- 

Let me know if you'd like more examples for these!

### **File Permissions & Ownership**

1. **`chmod`** - Change file permissions.
   - Example: `chmod 755 file.txt` (read/write/execute for owner, read/execute for others)

2. **`chown`** - Change file owner and group.
   - Example: `chown user:group file.txt`

3. **`chgrp`** - Change group ownership.
   - Example: `chgrp group file.txt`

---

### **System Information & Management**

1. **`uname -a`** - Display system information.
   - Example: `uname -a`

2. **`top`** - Display processes running on the system.
   - Example: `top`

3. **`ps aux`** - List all running processes.
   - Example: `ps aux`

4. **`df -h`** - Display disk space usage in human-readable format.
   - Example: `df -h`

5. **`free -m`** - Display memory usage.
   - Example: `free -m`

6. **`uptime`** - Show system uptime.
   - Example: `uptime`

7. **`reboot`** - Reboot the system.
   - Example: `sudo reboot`

8. **`shutdown`** - Shut down the system.
   - Example: `sudo shutdown -h now`

---

### **Network Management**

1. **`ifconfig`** - Display or configure network interfaces.
   - Example: `ifconfig`

2. **`ping`** - Send ICMP Echo requests to a host to check connectivity.
   - Example: `ping 8.8.8.8`

3. **`netstat`** - Show network connections, routing tables, and interface statistics.
   - Example: `netstat -tuln`

4. **`ip a`** - Display IP address information.
   - Example: `ip a`

5. **`nmap`** - Network scanner and vulnerability scanner.
   - Example: `nmap 192.168.1.1`

6. **`iwconfig`** - Configure wireless network interfaces.
   - Example: `iwconfig wlan0`

7. **`route`** - Display or modify the IP routing table.
   - Example: `route -n`

8. **`traceroute`** - Trace the route packets take to a destination.
   - Example: `traceroute google.com`

---

### **Package Management**

1. **`apt-get update`** - Update package information.
   - Example: `sudo apt-get update`

2. **`apt-get upgrade`** - Upgrade installed packages.
   - Example: `sudo apt-get upgrade`

3. **`apt-get install`** - Install a package.
   - Example: `sudo apt-get install nmap`

4. **`apt-get remove`** - Remove a package.
   - Example: `sudo apt-get remove nmap`

5. **`dpkg -l`** - List installed packages.
   - Example: `dpkg -l`

6. **`apt-cache search`** - Search for packages.
   - Example: `apt-cache search nmap`

---

### **User and Group Management**

1. **`adduser`** - Add a new user.
   - Example: `sudo adduser username`

2. **`usermod`** - Modify user accounts.
   - Example: `sudo usermod -aG sudo username`

3. **`passwd`** - Change user password.
   - Example: `passwd username`

4. **`groupadd`** - Add a new group.
   - Example: `sudo groupadd groupname`

5. **`groups`** - Display user groups.
   - Example: `groups username`

6. **`id`** - Display user and group information.
   - Example: `id username`

---

### **Kali Linux Security & Hacking Tools**

1. **`airmon-ng`** - Wireless network interface management.
   - Example: `sudo airmon-ng start wlan0`

2. **`aircrack-ng`** - Cracking WEP/WPA keys.
   - Example: `aircrack-ng capturefile.cap`

3. **`hydra`** - Password cracking tool.
   - Example: `hydra -l admin -P passwordlist.txt 192.168.1.1 ssh`

4. **`metasploit`** - Penetration testing framework.
   - Example: `msfconsole`

5. **`nmap`** - Network exploration tool and vulnerability scanner.
   - Example: `nmap -sP 192.168.1.0/24`

6. **`burpsuite`** - Web vulnerability scanner and proxy tool.
   - Example: `burpsuite`

7. **`nikto`** - Web server scanner.
   - Example: `nikto -h http://example.com`

8. **`netcat`** - Network utility for reading and writing data across network connections.
   - Example: `nc -lvp 1234`

---

### **Advanced Commands**

1. **`iptables`** - Command-line firewall utility.
   - Example: `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`

2. **`firewalld`** - Manage firewall rules.
   - Example: `sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent`

3. **`find`** - Search for files in a directory hierarchy.
   - Example: `find /home -name "*.txt"`

4. **`locate`** - Find files by name.
   - Example: `locate file.txt`

5. **`grep`** - Search text using patterns.
   - Example: `grep -r "error" /var/log/`

6. **`tar`** - Archive and compress files.
   - Example: `tar -czvf archive.tar.gz /path/to/directory`

7. **`chmod`** - Change file permissions.
   - Example: `chmod 777 file.txt`

8. **`sudo`** - Run commands with superuser privileges.
   - Example: `sudo shutdown -h now`

9. **`history`** - Show command history.
   - Example: `history`

10. **`wget`** - Download files from the internet.
    - Example: `wget http://example.com/file.zip`

11. **`curl`** - Transfer data from or to a server.
    - Example: `curl -O http://example.com/file.zip`

---

### **Disk and File System Management**

1. **`fdisk`** - Partition table manipulator.
   - Example: `sudo fdisk -l`

2. **`mount`** - Mount a file system.
   - Example: `sudo mount /dev/sda1 /mnt`

3. **`umount`** - Unmount file systems.
   - Example: `sudo umount /mnt`

4. **`lsblk`** - List information about block devices.
   - Example: `lsblk`

5. **`df`** - Display disk space usage.
   - Example: `df -h`

6. **`du`** - Estimate file space usage.
   - Example: `du -sh /path/to/dir`

---

This is just a brief overview of Kali Linux commands, from basic to advanced. As you dive deeper into cybersecurity, you will use these commands extensively for tasks like network penetration testing, vulnerability scanning, managing system configurations, and much more.