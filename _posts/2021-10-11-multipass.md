---
title: "Multipass"
date: 2021-10-11T15:34:30-04:00
categories:
  - blog
tags:
  - ubuntu
  - vm
  - linux
---
Multipass is a lightweight VM Manager for Linux, Windows and macOS. It's a powerful tool to easily create Ubuntu VM with minimum effort like issuing a single command. It uses KVM on Linux, Hyper-V on Windows and HyperKit on macOS to run the VMs with minimal overhead.

Multipass is a CLI to launch and manage VMs on Windows, Mac and Linux that simulates a cloud environment with support for cloud-init. In this post you will find most of the commonly used Multipass commands.

```bash
# find available images 
multipass find
  
# launch an instance using default current Ubuntu LTS 
multipass launch --name name-of-the-instance 
 
# launch a particular version of Ubuntu instance 
multipass launch --name name-of-the-instance 18.04
 
# launch an instance with specific hardware 
multipass launch -c 2 -m 2G -d 20G -n name-of-the-instance 
 
# stop and start instances 
multipass start name-of-the-instance <another-name>
multipass stop name-of-the-instance 
 
# enter shell of the instance 
multipass shell name-of-the-instance 
 
# list instances 
multipass list 
 
# delete the instance 
multipass delete name-of-the-instance 
 
# completely get rid of the instance 
multipass purge

# multipass service restart (macOS)
sudo launchctl stop com.canonical.multipassd
sudo launchctl start com.canonical.multipassd

##########################################################
             OTHER USEFUL PARAMETERS
##########################################################
delete # Delete instances
exec # Run a command on an instance
find # Display available images to create instances from
get # Get a configuration setting
help # Display help about a command
info # Display information about instances
launch # Create and start an Ubuntu instance
list # List all available instances
mount # Mount a local directory in the instance
purge # Purge all deleted instances permanently
recover # Recover deleted instances
restart # Restart instances
set # Set a configuration setting
shell # Open a shell on a running instance
start # Start instances
stop # Stop running instances
suspend # Suspend running instances
transfer # Transfer files between the host and instances
umount # Unmount a directory from an instance
version # Show version details
```
