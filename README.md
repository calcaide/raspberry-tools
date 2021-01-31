# Raspberry Pi Tools

This repository is not a guide, tutorial or something like this for that, already exists a fantastic [official documentation](https://www.raspberrypi.org/documentation/), is just a cheat sheet of commands, scripts and tools that I use for playing around with RPI.

Environment: Ubuntu server 20.04 LTS

## Network

### Static IP address assignment

Modify or create `/etc/netplan/99_config.yaml`.

*Change addresses and gateway4 by your actual ip's*

```yaml
network:
    version: 2
    renderer: networkd
    ethernets:
        eth0:
            addresses:
                - 10.10.10.10/24
            gateway4: 10.10.10.1
            nameservers:
                addresses: [10.10.10.1, 8.8.8.8]
```

After it, run: `$ sudo netplan apply`

[Ubuntu network documentation](https://ubuntu.com/server/docs/network-configuration)