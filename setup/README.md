# Setup 

This is just for setup the basics to use the Raspberry securely via ssh over the ethernet.

To me, this is the basic configuration because I need a display and a keyboard to do it. Once I applied the configuration, I can manage the raspberry with my laptop (or another device with a terminal) over the ssh.

*Most of these changes can be carried out by the `raspi-config` command.*



## Contents

- [Environment.](#environment).
- [Change locale, timezone and keyboard layout](#change-locale-timezone-and-keyboard-layout).
- [Change root password](#change-root-password).
- [Default user](#default-user).
- [Configure ethernet](#configure-ethernet).
- [Update and upgrade](#update-and-upgrade).
- [SSH access](#ssh-access).
- [Install No-Ip](#install-no-ip).
- [Expand file system](#expand-file-system).
- [Install LXDE GUI](#install-display-server).


### Environment

The environment (for now) is based in Raspbian Jessie Lite, then, depending on the purpose, I install some services or others.

For setup a basic environment, should [download the Raspbian Jessie Lite image][Download Jessie Lite] and format the sd card, follow these instructions depending on your host Operating system: [Linux][Linux format SD card], [Mac Os][Mac Os format SD card] or [Windows][Windows format SD card].


### Change locale, timezone and keyboard layout

Go to [Localisation](../localisation/README.md) section to see how to [change locale](../localisation/README.md#change-locale), [chane time zone](../localisation/README.md#change-time-zone) or [change keyboard layout](../localisation/README.md#change-keyboard-layout).


### Change root password

`$ sudo passwd root`

### Default user
For security and other reasons I like to delete default user.

Default:
user: `pi`
password: `raspberry`

Add new user:
`$ sudo adduser <username>`

Add to sudoers:
`$ sudo adduser <username> sudo`

Logout the actual session:
`$ logout`

Delete `pi` user:
`$ sudo userdel -r pi`.


### Configure ethernet

Go to [Configure ethernet](../network/README.md#configure-ethernet) in [network section](../network/README.md).

### Update and upgrade

Install and update to the latest files and packages, then clean it:

```
$ sudo apt-get update && apt-get upgrade

$ sudo apt-get dist-upgrade

$ sudo apt-get clean
```

Then reboot the system:

`$ sudo reboot`.


### SSH access

Go to [SSH access](../remote-access/README.md/#ssh-access) in remote access section, also [Passwordless SSH access](../remote-access/README.md#passwordless SSH access).


### Install No-Ip

Go to [Install No-Ip](../remote-access/README.md#install-no-ip) in [remote-access](../remote-access/README.md).

### Expand file system

It's important to expand the file system through raspi-config:

`$ sudo raspi-config` and then `1 Expand Filesystem`.


### Install LXDE GUI

Go to [GUI](../gui/README.md) and follow the table of contents.

- - - 

**References:**

- [Download Jessie lite][Download Jessie lite]
- Format SD Card:
	- [Linux format SD card][Linux format SD card]
	- [Mac Os format SD card][Mac Os format SD card]
	- [Windows format SD card][Windows format SD card]
	- [Add user to sudoers][Add user to sudoers]
- [Expand file system][Expand]

[Download Jessie lite]: https://www.raspberrypi.org/downloads/raspbian/

[Linux format SD card]: https://www.raspberrypi.org/documentation/installation/installing-images/linux.md
    
[Mac Os format SD card]: https://www.raspberrypi.org/documentation/installation/installing-images/mac.md

[Windows format SD card]: https://www.raspberrypi.org/documentation/installation/installing-images/windows.md

[Add user to sudoers]: http://askubuntu.com/questions/7477/how-can-i-add-a-new-user-as-sudoer-using-the-command-line

[Expand]: https://www.raspberrypi.org/documentation/configuration/raspi-config.md