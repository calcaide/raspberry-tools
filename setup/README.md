# Setup 

This is just for setup the basics to use the Raspberry securely via ssh over the ethernet. 

To me, this is the basic configuration because I need a display and a keyboard to do it. 
Once I applied the next configuration, I can manage the raspberry with my laptop (or other device with a terminal) over the ssh.

*Most of these changes can be carried out by the `raspi-config` command.*

## Contents

- [Enviorment](#enviorment).
- [Change locale, timezone and keyboard layout](#change-locale-timezone-and-keyboard-layout)
- [Default user](#default-user).
- [Configure ethernet](#configure-ethernet).
- [SSH access](#ssh-access).
- [Install No-Ip](#install-no-ip).
- [Install LXDE GUI]().


### Enviorment

The enviorment (for now) is based in Raspbian Jessie Lite, then, depending on the purpose, I install some services or others.

For setup a basic environment, should [download the Raspbian Jessie Lite image][Download Jessie Lite] and format the sd card, follow these instructions depending of your host Operating system: [Linux][Linux format SD card], [Mac Os][Mac Os format SD card] or [Windows][Windows format SD card].


### Change locale, timezone and keyboard layout

Go to [Localisation](../localisation/README.md) section to se how to [change locale](../localisation/README.md#change-locale), [chane time zone](../localisation/README.md#change-time-zone) or [change keyboard layout](../localisation/README.md#change-keyboard-layout).


### Default user
For security and other reasons I like to delete default users, but first I should to add one.

Add new user:
`sudo adduser <username>`

Add to sudoers:
`sudo adduser <username> sudo`

Logout the actual session:
`logout`

Delete `pi` user:
`sudo userdel -r pi`.


### Configure ethernet

Go to [Configure ethernet](../network/README.md#configure-ethernet) in [network section](../network/README.md).


### SSH access

Go to [SSH access](../remote-access/README.md/#ssh-access) in remote access section, also [Passwordless SSH access](../remote-access/README.md#passwordless SSH access).


### Install No-Ip

Go to [Install No-Ip](../remote-access/README.md#install-no-ip) in [remote-access](../remote-access/README.md).



- - - 

**References:**

- [Download Jessie lite][Download Jessie lite]
- Format SD Card:
	- [Linux format SD card][Linux format SD card]
	- [Mac Os format SD card][Mac Os format SD card]
	- [Windows format SD card][Windows format SD card]
	- [Add user to sudoers][Add user to sudoers]

[Download Jessie lite]: https://www.raspberrypi.org/downloads/raspbian/

[Linux format SD card]: https://www.raspberrypi.org/documentation/installation/installing-images/linux.md
    
[Mac Os format SD card]: https://www.raspberrypi.org/documentation/installation/installing-images/mac.md

[Windows format SD card]: https://www.raspberrypi.org/documentation/installation/installing-images/windows.md

[Add user to sudoers]: http://askubuntu.com/questions/7477/how-can-i-add-a-new-user-as-sudoer-using-the-command-line