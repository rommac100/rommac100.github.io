---
layout: post
title:  "Useful Linux Commands"
date:   2020-07-17
tags: [linux, computers]
post_url: /linux/2020-07-17-useful-linux-commands
---

# X11 Forwarding:
## enabling X11 forwarding (change for remote machine)
sshd config "/etc/ssh/ssh/sshd_config":
``` bash
X11Forading yes
X11DisplayOffset 10
X11UseLocalhost yes
AllowTcpForwarding yes
```
After that is enable ssh into your machine with -XY parameters
``` bash
ssh -XY username@hostname
```
And you should be able to launch a generic X11 application.

## Launch Desktop Environment
So far I have only tested xfce4 with X11 forwarding (I tried i3 but it would not work for a variety of reason unfortunately).
*Create X11 session: (issue on remote machine)*
**Install xnest via your package manager if you don't have it installed** 
```bash
Xnest :1 &
export DISPLAY=:1
```
Those command should make it possible to then just start the xfce4 session. Specifically it should create a black window on your host machine that will contain the xsession from your remote machine
```bash
xfce4-session
```
*Note that resizing the window is a bit finky so I recommend you execute the above command once the x11 window is at the desired size*
