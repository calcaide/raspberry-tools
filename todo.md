## COMPLETED
- Fix anchor links issue in setup/readme.md.


## ToDo
- Modify root README.
	- Explain that this is not a guide or something like this, is just a cheat sheat, bunch of scripts or things like that, just for playing around with RPI.

- Modify Setup.
	- Environment
		- Explaint that this cheat sheat is based on a Jessie lite.
	- Change keyboard layout: now should link to keyboard section.
	- Install LXDE GUI.
		- https://www.raspberrypi.org/forums/viewtopic.php?p=890408#p890408.
	- Default user: now should link to security section.
	- Configure ethernet: now should link to network section.
	- Configure ssh: now should link to remote-access section.

- Add keyboard section.
	- Move from setup: change keyboard layout.

- Add network section.
	- Configure ethernet.
	- Add configure wifi.

- Add security section.
	- Add default user (from setup).

- Add remote-access section.
	- Add SSH configuration. Then, change the setup readme, there is also a SSH section, should link to this one.
	- Add no-ip configuracion. To the same that with ssh configuration.
	- Add VNC article.
		- Idea: recommend some resolutions to use for a good UX working.
		- Suggest that any other VNC servers are there.
		- Choose one VNC server.
			- The one suggested by the oficial documentation looks good, because you should start a sesion. For security, looks pretty (at least, to me)
			first connect with SSH, start the service and then connect.

- Aliases
	- Echo temperature.
	- Start VNC server (start VNC service with preconfigured resolution).