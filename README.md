# PiHole on the Pogoplug Mobile (v4)

Why not just use a raspberry pi? 
1. The cost is less then $ 30 total and you have a fully working solution (almost half what you will spend with the pi) vs the raspberry pi where you need to by a power cable, Ethernet cable, case, SD card etc; all on top of the $ 35 pi. 
2. The Ethernet port is gigabit 1000MBs on the Pogoplug vs only 100MBs on the PI; SO TEN times faster!!! What?!!
3. Supports full SD cards, also micro SD cards via the SD adapter which is usually included when buying a micro SD Card. 
4. Already built to run in a headless mode.

Follow the steps below in order to setup your Pogoplug with PiHole.

## Pre-Requisites 

**PogoPlug v4 (Mobile)**

Roughly $5 (Plus Shipping) on [Ebay](https://www.ebay.com/itm/255982127104?mkcid=16&mkevt=1&mkrid=711-127632-2357-0&ssspo=PLV6qj2zTxa&sssrc=2047675&ssuid=Cjy1FHrMT0W&widget_ver=artemis&media=COPY)

**SD Card 2GB+**

32GB for roughly $8 on [Amazon](https://a.co/d/bqeT9nw)

**Soldering Iron**

As little as 9$ on [Amazon](https://a.co/d/6p36Kf7)

**USB to TTL Converter**

8$ on [Amazon](https://a.co/d/73xEUBs)

**Downloads**

Pogoplug Debian Image. [Taken from this repo](https://github.com/pepaslabs/pogoplug-v4-bodhi-rootfs-debian)

## Preparing the device

**Serial connection**

The only way to connect to the pogoplug nowadays is to solder some cables directly into the serial connection in between the SD Card slot and the Power Input.
https://youtu.be/oVc8QMos0AM?si=FOWqQUvnxVjbiOWY&t=35

**Follow this guide to allow SSH in your pogoplug**

Click on the [pastebin file](/pastebin.md) for my simplified version of this guide:
https://www.youtube.com/watch?v=SheuimfB6kQ 

He includes a lot of useful information. If you're new to this I recommend watching the whole video at least once.

## Installing the Operating System

**Install u-Boot**
Once you can SSH into the pogoplug and can run the command wget, install uboot
https://github.com/pepaslabs/pogoplug_mobile_uboot_installer

Once ready, power off your pogoplug and remove the sd card.

Format your sd card

**Download Debian and write to SD Card**

Use your favorite image tool to write the pogoplug debian image to it (I used win32diskimager) 

http://sourceforge.net/projects/win32diskimager/files/latest/download

plug your sd card into the pogoplug and boot. you will need to connect via SSH or Serial

user: root

password: _BLANK JUST PRESS ENTER_

## Configure Debian and Install Pihole:

**Update:**

`apt-get update`

`apt-get upgrade`

**Remove unneeded software:**

`apt-get remove apache*`

`apt-get autoremove`

**Adjust your timezone:**

`dpkg-reconfigure tzdata`

**Set a root password: (OPTIONAL, but recommended)**

`passwd`


### You're now ready to install pi-hole

Since installing Curl and Git does not work anymore (old version of Debian with many pages giving 404), the only option is to manually download the installer
https://docs.pi-hole.net/main/basic-install/

You now can follow the guides on PI HOLE for configuration (https://github.com/pi-hole/pi-hole)


