# PiHole on the Pogoplug Mobile (v4)

Why not just use a raspberry pi? 
1. The cost is less then $ 30 total and you have a fully working solution (almost half what you will spend with the pi) vs the raspberry pi where you need to by a power cable, Ethernet cable, case, SD card etc; all on top of the $ 35 pi. 
2. The Ethernet port is gigabit 1000MBs on the Pogoplug vs only 100MBs on the PI; SO TEN times faster!!! What?!!
3. Supports full SD cards, also micro SD cards via the SD adapter which is usually included when buying a micro SD Card. 
4. Already built to run in a headless mode.

Follow the steps below in order to setup your Pogoplug with PiHole.

### Items:

**Pogoplug v4 (Mobile) **

Roughly $15 on [Ebay](https://www.ebay.com/itm/255982127104?mkcid=16&mkevt=1&mkrid=711-127632-2357-0&ssspo=PLV6qj2zTxa&sssrc=2047675&ssuid=Cjy1FHrMT0W&widget_ver=artemis&media=COPY)

**SD Card 2GB+**

32GB for roughly $8 on [Amazon](https://a.co/d/bqeT9nw)

**Soldering Iron**

As little as 9$ on [Amazon] (https://a.co/d/6p36Kf7)

**USB to TTL Converter**
8$ on [Amazon] (https://a.co/d/73xEUBs)

### Downloads:

Pogoplug Debian img

https://github.com/pepaslabs/pogoplug-v4-bodhi-rootfs-debian

### Serial connection
The only way to connect to the pogoplug nowadays is to solder some cables directly into the serial connection in between the SD Card slot and the Power Input.
https://youtu.be/oVc8QMos0AM?si=FOWqQUvnxVjbiOWY&t=35


### First follow this guide to allow SSH in your pogoplug:

https://www.youtube.com/watch?v=SheuimfB6kQ and https://pastebin.com/mv1WdVdH
Follow those steps until you can SSH into your pogoplug

### Install u-booot
https://github.com/pepaslabs/pogoplug_mobile_uboot_installer


Once ready, power off your pogoplug and remove the sd card.

Format your sd card (I used SD Formmatter) 

https://www.sdcard.org/downloads/formatter_4/

### The section below I will not describe in detail how to use each software, please use google as there is already tons of guides.

use your favorite image tool to write the pogoplug debian image to it (I used win32diskimager) 

http://sourceforge.net/projects/win32diskimager/files/latest/download

use your favorite image tool to extend the the image to the full sd card (I used Gparted live)

http://gparted.org/livecd.php

plug your sd card into the pogoplug and boot. you will need to connect via SSH

user: root

password: _BLANK JUST PRESS ENTER_

Check to make sure it you are using the full sd card and have enough space. (after install roughly 1GB will be used)

`df -h`

### Update and install all needed all dependencies:

**Update:**

`apt-get update`

`apt-get upgrade`

**Install needed software:** This step will take the longest to install git

`apt-get install curl`

`apt-get install git-core`

**Remove unneeded software:**

`apt-get remove apache*`

`apt-get autoremove`

**Adjust your timezone:**

`dpkg-reconfigure tzdata`

**Set a root password:** (OPTIONAL, but recommended)

`passwd`

### Your now ready to install: 

`curl -sSL https://install.pi-hole.net | bash`


## Configure:
You now can follow the guides on PI HOLE for configuration (https://github.com/pi-hole/pi-hole)


