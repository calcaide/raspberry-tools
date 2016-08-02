# GUI

Installation of a lightweight GUI, [LXDE][LXDE] in this case and the minimum tools to work.

## Contents
- [Foundations tasks](#foundations-tasks).
- [Install display server](#install-display-server).
- [LXDE GUI](#lxde-gui).

### Foundations tasks

First [expand the file system](../setup/README.md/#expand-file-system).

Then, update and [upgrade the system](../setup/README.md/#update-and-upgrade).

### Install display server

Install [Xorg][Xorg] as a display server.

`$ sudo apt-get install --no-install-recommends xserver-xorg`.

Install [Xinit][Xinit] to launch the Xorg display server from the command line:

`$ sudo apt-get install --no-install-recommends xinit`.

### LXDE GUI

Also, install [LXTerminal][LXTerminal] as a terminal and [LXAppearance][LXAppearance] as a theme switcher.

`$ sudo apt-get install lxde-core lxterminal lxappearance`.

Finally, to launch Xorg display server:

`$ startx`.


- - -

**References:**

[Xorg][Xorg].

[Xinit][Xinit].

[LXTerminal][LXTerminal].

[LXAppearance][LXAppearance].

[Install LXDE reference][Install lxde reference].

[LXDE]: http://lxde.org/index.html

[Xorg]: https://www.x.org/wiki/

[Xinit]: https://en.wikipedia.org/wiki/Xinit

[LXTerminal]: http://wiki.lxde.org/en/LXTerminal

[LXAppearance]: http://wiki.lxde.org/en/LXAppearance

[Install lxde reference]: https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=133691