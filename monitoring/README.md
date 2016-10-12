# Monitoring

## Contents
- [Install Datadog](#install-datadog-agent).
	- [Autoruns on startup](#autoruns-on-startup).

### Install Datadog agent

Update local cache:  
`$ sudo apt update`

Install `sysstat`:  
`$ sudo apt install sysstat`

Navigate to the [Agent install Screen](https://app.datadoghq.com/account/settings#agent/source) in the DataDog Application ("from source" is already selected). Execute the installation command (copy from the app):    

`$ DD_API_KEY=<YOUR-API-KEY> sh -c "$(curl -L https://raw.githubusercontent.com/DataDog/dd-agent/master/packaging/datadog-agent/source/setup_agent.sh)"`

#### Autoruns on startup

Create a little bash script:

`$ nano ~/bash-scripts/datadog-startup.sh` (this depends on where you want to save the `.sh` file).

And looks something like this:

```shell
#!/bin/bash

cd /home/<your-user-name>/.datadog-agent

bin/agent
```

And now, create a unit file for systemd:

`$ nano /etc/systemd/system/datadog.service`

Should looks something like this:

```shell
[Unit]
Description= Datadog startup service.
After=network.target

[Service]
Type=idle
ExecStart=/home/<your-user-name>/bash-scripts/datadog-startup.sh

[Install]
WantedBy=multi-user.target
```

Then reboot `$ sudo reboot`.

And just enable the service at startup `$ systemctl enable datadog.service`.

**References**

- [Deploy Datadog agent on RPI](https://help.datadoghq.com/hc/en-us/articles/208163513-Deploying-the-Agent-on-RaspberryPI).
