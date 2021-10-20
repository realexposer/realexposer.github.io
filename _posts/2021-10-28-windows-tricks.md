---
title: "Windows Tricks"
date: 2021-10-28T15:34:30-04:00
categories:
  - blog
tags:
  - windows
  - tricks
---
## How to add an application or device or partition to send to menu (this is the menu accessed by right clicking on he desktop)?
Open Windows explorer (File explorer in Windows 8), and to go the address ‘shell:sendto’. Now place whatever the shortcut that needs to be displayed under send to menu.

## How identify the motherboard details from command line?
```bash
wmic baseboard get product,Manufacturer,version,serialnumber
```

## Wipe the drive’s partition table (source)
Open command prompt in administrator mode
```bash
diskpart
list disk
select disk # //# disk number based on the previous command output e.g: select disk 1
clean
exit
```
source: http://www.howtogeek.com/215349/how-to-remove-an-efi-system-partition-or-gpt-protective-partition-from-a-drive-in-windows/  

