---
title: "Raspberry Pi Tips/Tricks/Useful Links and Projects"
date: 2021-10-30T15:34:30-04:00
categories:
  - blog
tags:
  - 
---

## Useful projects links:
- [Awesome raspberry pi](https://github.com/careyer/awesome-raspberry-pi)

## Operating systems:
- [RetroPie](https://retropie.org.uk/) allows you to turn your Raspberry Pi or PC into a retro-gaming machine.
- Raspbian 
- Screenly 
- MotionEyeOS 
- RasPlex
- DietPi

## Media Center:
- [Xbian](http://www.xbian.org/what-is-xbian/) is a small, fast and lightweight media center distribution.
- OSMC
- LibreMC
- [Installing OpenElec](http://wiki.openelec.tv/index.php/Installing_OpenELEC_on_Raspberry_Pi#tab.3DWindows) on Raspberry Pi, [OpenElec Builds](http://openelec.tv/get-openelec)

## Interesting projects:
- [Magic Mirror](http://michaelteeuw.nl/post/83916869600/magic-mirror-part-vi-production-of-the), Mirrors designed [around the world](http://michaelteeuw.nl/post/111886383522/magic-mirrors-around-the-world), [GitHub repository](https://github.com/MichMich/MagicMirror).
- Photo Frame.
- NAS
  - [Raspberry Pi NAS](http://pimylifeup.com/raspberry-pi-nas/)
  - [Raspberry Pi NAS with redundancy using rsync](http://www.makeuseof.com/tag/turn-your-raspberry-pi-into-a-nas-box/)
  - How to make a Raspberry Pi NAS [Youtube video](https://www.youtube.com/watch?v=WXKkqDZi5jc)
- Raspberry Pi camera [live streaming and recording web interface](http://elinux.org/RPi-Cam-Web-Interface)
- [Configuring Plex in OSMC](https://forums.plex.tv/discussion/155081/plex-media-server-not-running-on-rapsberry-pi-2) (fixing the issue with some configuration - forum topic)
- [BlissFlixx](http://blissflixx.rocks/)

## Some of the useful pieces of information:
The default pi user on Raspbian is a sudoer. This gives the ability to run commands as root when preceded by sudo, and to switch to the root user with
```bash
sudo su
```
Launch Raspbian Config :
```bash
sudo raspi-config
```
## Compiling ffmpeg in Raspbian (with openssl):
```bash
sudo apt-get install openssh
sudo apt-get install libssl-dev
git clone https://git.ffmpeg.org/ffmpeg.git ffmpeg
cd ffmpeg
./configure --prefix=/home/pi/arm --enable-openssl
make
make install

# add the following to .bashrc file
export PATH=$PATH”:$HOME/arm/bin”
```


## Configuring OpenVPN:

```bash
sudo apt-get install network-manager-vpnc
sudo apt-get install openvpn network-manager-openvpn network-manager-openvpn-gnome
sudo /etc/init.d/networking restart
sudo openvpn --config ****.ovpn
```
 
The above will ask the username and password each time when you login. You can avoid this by storing your username and password in a text file. Following instructions below,
```bash
vim authorisation.txt

#enter the username and password as shown below
username
password

#now find the line with "auth-user-pass" within the *.ovpn file and replace is with the following
auth-user-pass authorisation.txt
```


