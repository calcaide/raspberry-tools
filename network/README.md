# Network

## Contents
- [Configure ethernet](#configure-ethernet).

### Configure ethernet

*Be aware, that is just for raspbian Jessie, don't use `/etc/network/interfaces`*

Type: `sudo nano /etc/dhcpcd.conf`

Go to the bottom of the document and add this:

```
interface eth0
static ip_address=192.168.1.X/24
static routers=192.168.1.1
static domain_name_servers=192.168.1.1 8.8.8.8
```

- - -

**References:**
- [Ethernet](https://www.raspberrypi.org/forums/viewtopic.php?p=798866#p798866).