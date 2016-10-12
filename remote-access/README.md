# Remote Access

## Contents
- [SSH access](#ssh-access).
- [Passwordless SSH access](#passwordless-ssh-access).
- [VNC](#vnc).
- [Install No-Ip](#install-no-ip).

### SSH access

By default the raspberry pi has the SSH server running and listening to the 22 port. Just to make sure that the service is up type: `sudo service ssh status`.

*If you don't receive a response, type `sudo raspi-config` then navigate to `ssh`, and select `Enable or disable ssh server`.*


### Passwordless SSH access
Absolutely based in [official documentation][Passwordless SSH access].

- [Check for existing SSH keys](#check-for-existing-ssh-keys).
- [Generate SSH keys](#generate-ssh-keys).
- Add authorized keys:
	- [Transfer public key from SSH client to SSH server](#transfer-public-key-from-ssh-client-to-ssh-server).
	- [Add public key to SSH server (from the server itself)](#add-public-key-to-ssh-server-from-the-server-itself)
- [Disable password logins](#disable-password-logins).

#### Check for existing SSH keys
`$ ls ~/.ssh`

**Remember**
`id_rsa`: Private.
`id_rsa.pub`: Public.

#### Generate SSH Keys

`$ ssh-keygen -t rsa -C <username>@<deviceId>`.

The  pattern `<username>@<deviceId>` could be whatever, like "Rpi #1" but I like to use `<username>@<deviceId>`.

Example: `$ ssh-keygen -t rsa -C`.

#### Transfer public key from SSH client to SSH server

Now, from a client machine:
`$ cat ~/.ssh/id_rsa.pub | ssh <username>@<IP-ADDRESS> 'cat >> .ssh/authorized_keys`'.

#### Add public key to SSH server (from the server itself)

`$ echo "<your public key>" >> ~/.ssh/authorized_keys`.

#### Disable password logins

Open SSH [config file][SSH config file]:
`$ sudo nano /etc/ssh/sshd_config`.

Find the line `#PasswordAuthentication yes`.

And change it to `PasswordAuthentication no`.

### VNC

Install [TightVNC][TightVNC] (vnc server):

`$ sudo apt-get install tightvncserver`

Run VNC server:

`$ tightvncserver`

Start vnc session:

`$ vncserver :1 -geometry 1024x768 -depth 24`

Stop vnc session: 

`$ vncserver -kill :1`


### Install No-Ip

Create temporal dir (for installation files):

`$ mkdir /home/userName/noip`

`$ cd /home/userName/noip`

Download the client and unzip it:

`$ wget https://www.noip.com/client/linux/noip-duc-linux.tar.gz`

`$ tar vzxf noip-duc-linux.tar.gz`

Enter installation directory:

`$ cd noip-2.1.9-1`

*the version could be different, verify first and change it if need it*

Compile and install:

`$ sudo make`  
`$ sudo make install`

**Auto runs when startup raspberry Pi (with [systemd][systemd]):**

First, create unitfile for systemd (I took these [from here][noip.service]):

`$ nano /etc/systemd/system/noip.service`

And looks something like this:


```shell
[Unit]
Description=No-IP dynamic DNS update client
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/bin/noip2
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Then reboot `$ sudo reboot`.

Check the service status:

`$ systemctl status noip.service`

Start the service:

`$ sudo systemctl start noip.service`

Enable service at startup:

`$ sudo systemctl enable noip.service`

- - -

**References**

- [SSH access][SSH access]
- [Passwordless SSH access][Passwordless SSH access]
- [Disable password logins][Disable password logins]
- [SSH config file][SSH config file]
- [Vnc][vnc]
- [TightVNC][TightVNC]
- [Install No-ip][install no-ip]
- [Systemd][systemd]
- [Create noip systemd service][noip.service]


[SSH access]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md

[Passwordless SSH access]: https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md

[Disable password logins]: http://raspberrypi.stackexchange.com/a/1687

[SSH config file]: http://www.tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/chap15sec122.html

[VNC]: https://www.raspberrypi.org/documentation/remote-access/vnc/README.md

[TightVNC]: http://www.tightvnc.com

[install no-ip]: http://www.noip.com/support/knowledgebase/installing-the-linux-dynamic-update-client/

[systemd]: https://wiki.archlinux.org/index.php/Systemd

[noip.service]: https://www.raspberrypi.org/forums/viewtopic.php?f=53&t=18569