---
title: "Linux Basic Commands"
date: 2021-10-22T15:34:30-04:00
categories:
  - blog
tags:
  - linux
---

Linux is a family of open-source free operating systems built using the Linux kernel. Linux is an incredibly powerful operating system when compared to other types of operating system for certain tasks, mostly command line based tasks. This means, it has a steep learning curve and you will be learning new things everyday. In this post I will be listing some of the basic commands that you might find useful to get started and to perform day to day activities in Linux.

### Identifying the IP address
```bash
ip addr show
ifconfig
```

### Changing the default password
```bash
passwd
```

### Display the amount of disk space available
```bash
df -h # -h: human readable output format
```

### scp copy
```bash
scp /path/to/file username@a:/path/to/destination
scp username@b:/path/to/file /path/to/destination

### Executing a command at a fixed interval using watch command
watch -n x command
# "x" is the repeat time in seconds;"command" is the command that you want to execute
```

### Running a command at a fixed interval
```bash
while true; do
cmd >> output.txt
sleep 2
done

while true; do sleep 2; cmd >>output.txt; done &
```

### Running a command in background
```bash
nohup command &
```

### Show the list of installed packages in Ubuntu or Debian
```bash
dpkg --get-selections
```

### Check the capacity of a directory
```bash
du -sh /path/directory
# h: human readable output; s: total disk space used by the directory
```

### Installing ffmpeg from ppa depository (add ppa to apt apt-get and install) - (source)
```bash
sudo add-apt-repository ppa:mc3man/trusty-media
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install ffmpeg
```

### Get the version of the libav-tools (source)
```bash
apt-cache search libav | grep libav
```

### Execute modified command when called by adding alias to the bashrc file (source)
```bash
echo "alias ls='ls -alh'" | tee -a ~/.bashrc; . ~/.bashrc
# alternatively, you can edit this file by opening this file from your home directory
vim .bashrc
```

### Installing OpenVPN client and import *.ovpn (Windows) file to configure
```bash
sudo apt-get install openvpn
sudo apt-get install network-manager-openvpn-gnome
# Now goto the network settings on the system tray -> “vpn connections” -> “configure vpn” ->
# “Add” -> select “Import saved VPN configuration” from the drop down list - > “create” ->
# select the *.ovpn file -> finally, type the username and password and click “ok”.
# Now go to the network settings and connect to the configured VPN server.
```

### Counting the number of files in a directory and sub-directories (source)
```bash
find . -type f | wc -l
# . - this directory and all subdirectories
# -type f - find all files
# | - piped into wc - word count and the -l - tells to count the lines from wc

# or

find . | wc -l
# this counts the files and directories within the current directory.
```

### Extract a process detail from top command based on process name
```bash
top -c -p $(pgrep -d',' -f ffmpeg)
```

### Spitting a MP3 files into multiple files (source)
```bash
ffmpeg -i 01.mp3 -f segment -segment_time 100 -c copy 01_%03d.mp3
```

### Joining MP3 files to a single track:[pre class="brush:bash"]
```bash
cat *.mp3 > out.mp3
```

### Copy/Sync a Directory on Local Computer
```bash
rsync -avzh /root/rpmpkgs /tmp/backups/
```

### chmod
```bash
chmod 700 myDir #7-user; 0:Group; 0: Others - read(4), write(2), execute(1)
# Permission rwx Binary
#7 read, write and execute rwx 111
#6 read and write rw- 110
#5 read and execute r-x 101
#4 read only r-- 100
#3 write and execute -wx 011
#2 write only -w- 010
#1 execute only --x 001
#0 none --- 000
```

### List all the directories with sizes
```bash
du -sh *
du: disk usage
# -s: Display an entry for each specified file
# -h: human readable format
du -sh * | sort -n # sort folders by size
du -sh * | tail -r # sort by largest first
```

### List all the processes associated with a process-name
```bash
ps -fC process-name
```

### Deleting an entry from history
```bash
history -d line_number
```

### List all the installed packages
```bash
apt list --installed
```

### Changing password of another user
```bash
sudo passwd user_name
```

### Terminal execute commands as another user
```bash
sudo su user_name
```

### Find UID of a user
```bash
id -u user_name
```

### Find GID of a user
```bash
id -g user_name
```

### Find all the groups a user belongs to
```bash
id -G user_name
groups
groups username
```

### Find all the groups associated with UID
```bash
id user_name
```

### Disable sudo password for a particular user
```bash
#create a file in /etc/sudoers.d for example
sudo vim /etc/sudoers.d/dont_prompt_user
#add the following to the above file
user_name ALL=(ALL) NOPASSWD:ALL
```

### Renaming all files in a folder (Amend for eg: unix_)
```bash
rename 's/^/Unix_/' *
```

### List the number of threads for a process ID
```bash
ps -o nlwp processID
cat /proc/processID/status | grep Threads
ls /proc/processID/task/ | wc -l
```

### Setting time zone from terminal
```bash
sudo dpkg-reconfigure tzdata
```

### Syncing files using rsync
```bash
rsync -aqv -e "ssh -T -o Compression=no -x" user@10.1.1.1:/source/path/* /destination/path/
rsync -aqvzh source/path destination/path --delete
```

### Importing ssh key from github
```bash
ssh-import-id-gh user_id
```

### Changing default ssh port
```bash
vi /etc/ssh/sshd_config
#locate the Port 22 line and change it
service sshd restart
```

### Compressing PDF files using ghostscript
```bash
sudo apt install ghostscript
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/prepress -dNOPAUSE -dQUIET -dBATCH -sOutputFile=compressed_PDF_file.pdf input_PDF_file.pdf
# some example dPDSETTINS: /prepress /printer /ebook /screen
```

### Ubuntu .deb package installation/uninstallation
```bash
#installing
sudo dpkg -i package_file.deb

#uninstalling
#list the packages installed with name urserver
sudo dpkg -l '*urserver*'

#remove the package itself (without the configuration files
sudo dpkg -r urserver

#delete (purge) the package completely (with configuration files)
sudo dpkg -P urserver

#check if the package has been removed successfully
sudo dpkg -l urserver
```

### Check CPU microarchitecture
```bash
cat /sys/devices/cpu/caps/pmu_name
```

## Debug in bash
### Enable
``set -x``
### Dissable
``set +x``
