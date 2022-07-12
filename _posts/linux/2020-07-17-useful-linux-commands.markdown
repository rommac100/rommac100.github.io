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

# USB bus Hunting
A bit more esoteric but in case you are doing usb passthrough to a vm lsusb (not installed by default on most distros) is critical for determining it. 
<a/>
Specifically, the following command prints your buses + devices and the pci lanes for the various busses
```bash
lsusb.py -ciu 
```

Example output:
```
usb5              1d6b:0002 09 1IF  [USB 2.00,   480 Mbps,   0mA] (xhci-hcd 0000:0b:00.3) hub
  5-1               0424:2512 09 1IF  [USB 2.00,   480 Mbps,   2mA] (Microchip Technology, Inc. (formerly SMSC) USB 2.0 Hub) hub
    5-1.1             0424:2602 09 1IF  [USB 2.00,   480 Mbps,   2mA] (Microchip Technology, Inc. (formerly SMSC) USB 2.0 Hub) hub
      5-1.1.1           0424:2228 00 1IF  [USB 2.00,   480 Mbps,   2mA] (Microchip Technology, Inc. (formerly SMSC) 9-in-2 Card Reader 080521109942)
        5-1.1.1:1.0         (IF) 08:06:50 2EPs (Bulk-Only) usb-storage host10 (sdh sdg)
  5-2               046d:c332 00 2IFs [USB 2.00,    12 Mbps, 300mA] (Logitech Gaming Mouse G502 047D38653935)
    5-2:1.0           (IF) 03:01:02 1EP  (Mouse) usbhid hidraw4 (hid-generic) input14 (hid-generic)
    5-2:1.1           (IF) 03:00:00 1EP  (None) usbhid hidraw5 (hid-generic) input15 (hid-generic)
  5-3               16c0:047d 00 4IFs [USB 2.00,    12 Mbps, 100mA] (Soarer Soarer's Keyboard Converter)
    5-3:1.0           (IF) 03:01:01 1EP  (Keyboard) usbhid hidraw0 (hid-generic)
    5-3:1.1           (IF) 03:00:00 1EP  (None) usbhid hidraw1 (hid-generic)
    5-3:1.2           (IF) 03:00:00 1EP  (None) usbhid hidraw2 (hid-generic) input18 (hid-generic)
    5-3:1.3           (IF) 03:00:00 2EPs (None) usbhid hidraw3 (hid-generic)
  5-4               1235:8211 ef 5IFs [USB 2.10,   480 Mbps, 500mA] (Focusrite Scarlett Solo USB Y7EZUJW1CDCC81)
    5-4:1.0           (IF) 01:01:20 0EPs (Audio) snd-usb-audio sound/card1
    5-4:1.1           (IF) 01:02:20 1EP  (Audio) snd-usb-audio
    5-4:1.2           (IF) 01:02:20 1EP  (Audio) snd-usb-audio
    5-4:1.3           (IF) ff:01:20 1EP  (Vendor Specific Class)
    5-4:1.4           (IF) 08:06:50 2EPs (Bulk-Only) usb-storage host11 (sdi)
```
In conjuction with lspci, it should be quite easy to move around devices in order to more easily pass devices through

# Memory Cache Clearing
 Although you shouldn't encounter this issue (probably related to a memory leak) this command is useful for clearing large memory caches. In my case I get sometimes up to 10 gigs cached up for not real apparent reason.

```bash
# sync; echo 1 > /proc/sys/vm/drop_caches

```
