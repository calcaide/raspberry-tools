# Remote Access

## Contents
- [SSH access](#ssh-access).
- [Passwordless SSH access](#passwordless-ssh-access).
- [Install No-Ip](#install-no-ip).

### SSH access

By default the raspberry pi has the SSH server running and listening to the 22 port. Just to make sure that the service is up type: `sudo service ssh status`.

*If you don't receive a response, type `sudo raspi-config` then navigate to `ssh`, and select `Enable or disable ssh server`.*


### Passwordless SSH access
Absolutely based in [official documentation][Passwordless SSH access].

- [Check for existing SSH keys](#check-for-existing-ssh-keys).
- [Generate SSH keys](#generate-ssh-keys).
- [Transfer public key from SSH client to SSH server](#transfer-public-key-from-ssh-client-to-ssh-server).
- [Disable password logins](#disable-password-logins).

#### Check for existing SSH keys
`ls ~/.ssh`

**Remember**
`id_rsa`: Private.
`id_rsa.pub`: Public.

#### Generate SSH Keys

`ssh-keygen -t rsa -C <username>@<deviceId>`.

The  pattern `<username>@<deviceId>` could be whatever, like "Rpi #1" but I like to use `<username>@<deviceId>`.

Example: `ssh -keygen -t rsa -C`.

#### Transfer public key from SSH client to SSH server

Now, from a client machine:
`cat ~/.ssh/id_rsa.pub | ssh <username>@<IP-ADDRESS> 'cat >> .ssh/authorized_keys`.

#### Disable password logins

Open SSH [config file][SSH config file]:
`sudo nano /etc/ssh/sshd_config`.

Find the line `#PasswordAuthentication yes`.


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

Add permissions: `sudo chmod +x /etc/init.d/noip2`.

Register the script to be run at start-up: `sudo update-rc.d noip2 defaults`.

- - -

**References**
- [SSH access](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md).
[Passwordless SSH access]:[https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md].
[Disable password logins](http://raspberrypi.stackexchange.com/a/1687).
[SSH config file](http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap15sec122.html).
- Install No-ip: [Post 1](http://raspberrypihelp.net/tutorials/29-raspberry-pi-no-ip-tutorial), [Post 2](http://www.stuffaboutcode.com/2012/06/raspberry-pi-run-program-at-start-up.html)