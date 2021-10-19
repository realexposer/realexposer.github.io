---
title: "Mounting a Network Drive in Linux"
date: 2021-10-25T15:34:30-04:00
categories:
  - blog
tags:
  - linux
---
In this post we will look at how mount a network drive in Ubuntu. Install CIFS:  
```bash
sudo apt-get install cifs-utils
```
Mount password protected network folders  
Using a text editor, create a file for your remote servers logon credential:  
```bash
gedit ~/.smbcredentials
```
Enter your Windows username and password in the file:  
```bash
username=msusername
password=mspassword
```
Save the file, exit the editor.  
Change the permissions of the file to prevent unwanted access to your credentials:  
```bash
chmod 600 ~/.smbcredentials
```
Then edit your /etc/fstab file (with root privileges) to add this line (replacing the insecure line in the example above, if you added it):  
```bash
//servername/sharename /media/windowsshare cifs credentials=/home/ubuntuusername/.smbcredentials,iocharset=utf8,sec=ntlm 0 0
```
If you want to mount the SMB drive with write access  
```bash
//servername/sharename /media/windowsshare cifs credentials=/home/ubuntuusername/.smbcredentials,uid=1000,gid=1000,iocharset=utf8,sec=ntlm 0 0
```
Save the file, exit the editor.  
Finally, test the fstab entry by issuing:  
```bash
sudo mount -a
```
More secure way of login in: Following command will ask the password when entered:  
```bash
sudo mount -t cifs //10.1.1.1/network_share /media/mount_directory -o sec=ntlmssp,uid=1000,gid=1000,user=username
```
Source: https://wiki.ubuntu.com/MountWindowsSharesPermanently