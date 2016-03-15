# Setup 

This is just for setup the basics to use the Raspberry securely via ssh over the ethernet. 

To me, this is the basic configuration because I need a display and a keyboard to do it. 
Once I applied the next configuration, I can manage the raspberry with my laptop (or other device with a terminal) over the ssh.

*Most of these changes can be carried out by the `raspi-config` command.*

## Contents

- [Enviorment](#enviorment).
- [Configure ethernet](#configure-ethernet).

- [Default user](#default-user).
- [Install LXDE GUI]().

- [Change locale](#change-locale).
- [Change keyboard layout](#chnage-keyboard-layout).
- [Change time zone](#change-time-zone).


- [Configure SSH access](#configure-ssh-access).
- [Install No-Ip](#install-no-ip)


### Enviorment

The enviorment (for now) is based in Raspbian Jessie Lite, then, depending on the purpose, I install some services or others.

For setup a basic environment, should [download the Raspbian Jessie Lite image][Download Jessie Lite] and format the sd card, follow these instructions depending of your host Operating system: [Linux][Linux format SD card], [Mac Os][Mac Os format SD card] or [Windows][Windows format SD card].

### Configure ethernet

Go to [Configure ethernet](network/README.md#configure-ethernet) in network section.

### Default user
Before connect the rpi to internet, you must add a user and delete the default. If want to keep the pi user, just change the password typing `passwd`.

Add new user:
`sudo adduser carlos`

Add to sudoers:
`sudo visudo`

Bellow `root` add `carlos   ALL = NOPASSWD: ALL`
```
# User privilege specification
root    ALL=(ALL:ALL) ALL
carlos  ALL = NOPASSWD: ALL
```

Logout the actual session: `logout`.

Delete `pi` user: `sudo userdel -r pi`.1

### Change locale

Type: `sudo dpkg-reconfigure locales`. Then, select your locale.


### Change keyboard layout

Type: `sudo dpkg-reconfigure keyboard-configuration`


### Change time zone

Type: `sudo dpkg-reconfigure tzdata`



### Configure ethernet
Type: `sudo nano /etc/network/interfaces`.

Replace the line `iface eth0 inet manual (or dhcp)` with:

```
iface eth0 inet static
address 192.168.1.6
netmask 255.255.255.0
gateway 192.168.1.1
```

### Configure SSH access

By default the raspberry pi has the SSH server running and listening to the 22 port. Just to make sure that the service is up type: `sudo service ssh status`.

*If you don't receive a response, type `sudo raspi-config` then navigate to `ssh`, and select `Enable or disable ssh server`*


### Install No-Ip

Create temporal dir (for installation files):

`mkdir /home/userName/noip`

`cd /home/userName/noip`

Download the client and unzip it:

`wget https://www.noip.com/client/linux/noip-duc-linux.tar.gz`

`tar vzxf noip-duc-linux.tar.gz`

Compile and install:

`sudo make`
`sudo make install`

Auto runs when startup raspberry Pi:

`sudo nano /etc/init.d/noip2`

Basic script:

```
#! /bin/bash
### BEGIN INIT INFO
# Provides:             noip
# Required-Start:       $remote_fs $syslog
# Required-Stop:        $remote_fs $syslog
# Default-Start:        2 3 4 5
# Default-Stop:         0 1 6
### END INIT INFO

sudo /usr/local/bin/noip2
```

Add permissions: `sudo chmod +x /etc/init.d/noip2`

Register the script to be run at start-up: `sudo update-rc.d noip2 defaults`


- - - 

**References:**

- [Download Jessie Lite](https://www.raspberrypi.org/downloads/raspbian/)
- Format SD Card
	- [Linux format SD card](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md)
	- [Mac Os format SD card](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md).
	- [Windows format SD card](https://www.raspberrypi.org/documentation/installation/installing-images/windows.md).

- [Users](https://www.raspberrypi.org/documentation/linux/usage/users.md).
- [Ethernet](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=38825).
- [SSH access](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md).
- Install No-ip: [Post 1](http://raspberrypihelp.net/tutorials/29-raspberry-pi-no-ip-tutorial), [Post 2](http://www.stuffaboutcode.com/2012/06/raspberry-pi-run-program-at-start-up.html)
