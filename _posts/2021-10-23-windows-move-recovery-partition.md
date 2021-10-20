---
title: "Windows: How to Move Recovery Partition on Windows 10"
date: 2021-10-23T15:34:30-04:00
categories:
  - blog
tags:
  - windows
  - windows10
---
According to MS's documentation, [capture-and-apply-windows-system-and-recovery-partitions](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/capture-and-apply-windows-system-and-recovery-partitions), the recovery partition can be captured and applied to a new partition. I have made it to work on my windows 10 PC.  

Warning 1: You must know what the following commands do before you execute them. Check the link above and MS's documentation for [diskpart](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/diskpart), [dism](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/dism-image-management-command-line-options-s14) and [reagentc](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/reagentc-command-line-options).  

Warning 2: Check disk numbers, partition numbers and volume letters carefully before executing commands.  
Use diskpart to find current recovery partition and assign a driver letter(eg. O) to it (following should be entered into diskpart terminal):  

```bash
DISKPART> list disk 

DISKPART> select disk <the-number-of-disk-where-current-recovery-partition-locate> 

DISKPART> list partition 

DISKPART> select partition <the-number-of-current-recovery-partition> 

DISKPART> assign letter=O
```
Create an image file from current recovery partition:
```bash
Dism /Capture-Image /ImageFile:C:\recovery-partition.wim /CaptureDir:O:\ /Name:"Recovery"
```
Apply the created image file to another partition(eg. N) that will become the new recovery partition:
```bash
Dism /Apply-Image /ImageFile:C:\recovery-partition.wim /Index:1 /ApplyDir:N:\
```
Register the location of the recovery tools:
```bash
reagentc /disable 

reagentc /setreimage /path N:\Recovery\WindowsRE 

reagentc /enable
```
Use diskpart to hide the recovery partition:  
For UEFI:  
```bash
DISKPART> select volume N 

DISKPART> set id="de94bba4-06d1-4d40-a16a-bfd50179d6ac" 

DISKPART> gpt attributes=0x8000000000000001 

DISKPART> remove
```
For BIOS:  
```bash
DISKPART> select volume N 

DISKPART> set id=27 

DISKPART> remove
```
Reboot the computer, now the new recovery partition should be working
(Optional) Delete the old recovery partition:  
```bash
DISKPART> select volume O 

DISKPART> delete partition override
```
(Optional) Check if the recovery partition is working:  
Show the current status:  
```bash
reagentc /info
```
Specifies that Windows RE starts automatically the next time the system starts:
```bash
reagentc /boottore
```
Reboot the computer and do your stuff in Windows RE (eg. enter CMD and run some tools)  

source: https://itectec.com/superuser/how-to-move-the-recovery-partition-on-windows-10  