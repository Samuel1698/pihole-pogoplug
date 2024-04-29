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

I've included the image files for both [Windows](https://github.com/Samuel1698/pihole-pogoplug/releases/download/Latest/Debian-jessie-3.18.5-pogoplug-v4-20151110-disk-image.4GB.img.zip) and [Linux](https://github.com/Samuel1698/pihole-pogoplug/releases/download/Latest/Debian-jessie-3.18.5-pogoplug-v4-20151110-disk-image.dd.gz) from the repo below, in case it goes down.

[PogoPlug v4 bodhi rootfs debian](https://github.com/pepaslabs/pogoplug-v4-bodhi-rootfs-debian)

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

Recommended to restart the device

## Configure Debian and Install Pihole:

**Changing the source files for apt:**

Since Debian 8 is no longer supported, we need to change the source file for apt-get
Open it by typing `nano /etc/apt/sources.list`
```
deb [trusted=yes] http://archive.debian.org/debian/ jessie main
deb-src [trusted=yes] http://archive.debian.org/debian/ jessie main

deb [trusted=yes] http://archive.debian.org/debian-security/ jessie/updates main contrib non-free
deb-src [trusted=yes] http://archive.debian.org/debian-security/ jessie/updates main contrib non-free
```


**Update:**

`apt-get update`

`apt-get upgrade`

**Set a root password: (OPTIONAL, but recommended)**

`passwd`

**Upgrade from Debian 8 to Debian 9**

As root user, edit /etc/apt/sources.list - change all occurrences of jessie to stretch

then run these commands
```
apt-get update
apt-get upgrade
apt-get dist-upgrade
reboot
```

**Upgrade to Debian 10**

If you apt-get dist-upgrade from jessie to stretch and it "bricks" your 'plug, it is probably due to fsck not being able to find /dev/root:

```
[....] Checking file systems...fsck from util-linux 2.29.2
fsck.ext3: No such file or directory while trying to open /dev/root
Possibly non-existent device?
fsck exited with status code 8
failed (code 8).
[FAIL] File system check failed. A log is being saved in /var/log/fsck/checkfs if that location is writable. Please repair the file system manually. ... failed!
[warn] A maintenance shell will now be started. CONTROL-D will terminate this shell and resume system boot. ... (warning).
Give root password for maintenance
(or press Control-D to continue):
```
You can fix this by placing your SD card into a laptop and editing /etc/fstab. Replace /dev/root with /dev/mmcblk0p1 (if you boot from SD card).

Boot the plug and you should be able to log in with 'root' and your selected password.

Modify once again the 'etc/apt/sources.list`. This time, we're changing 'stretch' to 'buster' and adding a few sources

```
deb http://archive.debian.org/debian buster main contrib non-free
deb-src http://archive.debian.org/debian buster main contrib non-free

deb http://archive.debian.org/debian buster-updates main contrib non-free
deb-src http://archive.debian.org/debian buster-updates main contrib non-free

deb http://archive.debian.org/debian buster-backports main contrib non-free
deb-src http://archive.debian.org/debian buster-backports main contrib non-free

deb http://security.debian.org/debian-security/ buster/updates main contrib non-free
deb-src http://security.debian.org/debian-security/ buster/updates main contrib non-free
```

Then run these commands again
```
apt-get update
apt-get upgrade
apt-get dist-upgrade
reboot
```

### You're now ready to install pi-hole

https://docs.pi-hole.net/main/basic-install/

You now can follow the guides on PI HOLE for configuration (https://github.com/pi-hole/pi-hole)


