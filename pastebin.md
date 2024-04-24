## Important Information
Serial connection is at J11, left of SD as you face SD opening.

Pins are 0V, Rx, Tx (moving right to left from SD).

Do not connect +V pin. Make sure your serial device is 3.3V, not 5V. Baud rate is 115200.



## Connect

>screen /dev/ttyUSB0 115200

or

>stty raw -echo < /dev/ttyUSB0

>cat /dev/ttyUSB0


### remount / as read/write

>mount -o remount,rw /`


### change root password


>passwd root


### Start telnetd or ssh server (both are already there)

startup script can be found here

Enable dropbear and telnet and disable pogo services 'hbmgr.sh':

Comment out the 'if' and 'fi' portion of this file and 'hbmgr.sh'


>vi /etc/init.d/rcS



## SSH DropBear

The version of Dropbear on this device is old

it uses an old/less secure encryption that your client might not like

you can override this on your client side like this


>ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 root@192.168.1.104


there is no sftp server, but you can scp like this


>scp -oKexAlgorithms=+diffie-hellman-group1-sha1 <file> root@192.168.1.104:
