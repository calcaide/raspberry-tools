# Setup 

This is just for setup the basics to use the Raspberry securely via ssh over the ethernet. 

To me, this is the basic configuration because I need a display and a keyboard to do it. 
Once I applied the next configuration, I can manage the raspberry with my laptop (or other device with a terminal) over the ssh.

*Most of these changes can be carried out by the `raspi-config` command.*

## Contents

- [Change locale](change-locale).
- [Change keyboard layout](chnage-keyboard-layout).
- [Change time zone](change-time-zone).


### Change locale

Type: `sudo dpkg-reconfigure locales`. Then, select your locale.

### Change keyboard layout

Type: `sudo dpkg-reconfigure keyboard-configuration`

### Change time zone

Type: `sudo dpkg-reconfigure tzdata`