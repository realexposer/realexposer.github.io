---
title: "Mounting Drives on Linux"
date: 2021-10-24T15:34:30-04:00
categories:
  - blog
tags:
  - linux
---
In this post, we will look at different mounting options.  
### Mounting external drives in read-write mode
source: http://www.cyberciti.biz/datacenter/linux-unix-bsd-osx-cannot-write-to-hard-disk/
```bash
mount -o remount,rw /media/"disk_name" 
```
Replace disk_name with the drive name  

### List the disk formatted in NTFS
```bash
fdisk -l | grep NTFS
```
### Mount the drive formatted in NTFS
```bash
sudo mount -t ntfs-3g /dev/NTFS_PARTITION /mount/DIRECTORY
```
Where, NTFS_PARTITION is the partition of the drive you want to mount not the device and DIRECTORY is the the location where you want to mount  

### Rename USB drive in Ubuntu (source)
Firstly unmount the device  
```bash
sudo unmount /dev/sdb1
```

```bash
sudo ntfslabel /dev/sdb1 my_external
```
Now remove the device and put back again and mount it  
### Unmount a busy drive
```bash
sudo umount -l /PATH/OF/BUSY-DEVICE
```
### List block devices
```bash
lsblk
```
With some additional parameters
```bash
sudo lsblk --output NAME,FSTYPE,LABEL,UUID,MODE
```
### Mounting LUKS encrypted disks
Install crytsetup  
```bash
sudo apt-get install cryptsetup
```
Find the full path of your device (e.g. /dev/sda)  
```bash
sudo fdisk -l
```
Unlock encrypted disk and create a mapper  
```bash
sudo cryptsetup luksOpen /dev/sda first_disk
```
You can check the status of the above mapper using the following command  
```bash
sudo cryptsetup -v first_disk
```
Mount the mapper  
```bash
sudo mount /dev/mapper/first_disk /mount/mount_directory
```
### Unmounting and lock LUKS encrypted partition
Unmount the disk  
```bash
sudo umount /mount/mount_directory
```
Lock the partition using cryptsetup  
```bash
sudo cryptsetup luksClose /dev/mapper/first_disk
```
source: https://medium.com/@amritanshu16/how-to-mount-luks-encrypted-disk-in-raspbian-821b0a56c18e
