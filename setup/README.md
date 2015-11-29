# Setup 

This is just for setup the basics to use the Raspberry securely via ssh over the ethernet. 

To me, this is the basic configuration because I need a display and a keyboard to do it. 
Once I applied the next configuration, I can manage the raspberry with my laptop (or other device with a terminal) over the ssh.

*Most of these changes can be carried out by the `raspi-config` command.*

## Contents

- [Change locale](change-locale).
- [Change keyboard layout](chnage-keyboard-layout).
- [Change time zone](change-time-zone).
- [Default user](default-user).
- [Configure ethernet](configure-ethernet).


### Change locale

Type: `sudo dpkg-reconfigure locales`. Then, select your locale.


### Change keyboard layout

Type: `sudo dpkg-reconfigure keyboard-configuration`


### Change time zone

Type: `sudo dpkg-reconfigure tzdata`


### Default user
Before connect the machine to internet, you must add a user and delete the default. If want to keep the pi user, just change the password typing `passwd`.

Add new user:
`sudo adduser carlos`

Add to sudoers:
`sudo visudo`

Bellow `root` add `carlos   ALL = NOPASSWD: ALL`
```
# User privilege specification
root  ALL=(ALL:ALL) ALL
carlos   ALL = NOPASSWD: ALL
```

Logout the actual session: `logout`.

Delete `pi` user: `sudo userdel -r pi`.


### Configure ethernet
Type: `sudo nano /etc/network/interfaces`.

Replace the line `iface eth0 inet manual (or dhcp)` with:

```
iface eth0 inet static
address 192.168.1.6
netmask 255.255.255.0
gateway 192.168.1.1
```