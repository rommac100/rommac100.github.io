---
layout: post
title:  "Laptop Issues and Fixes"
date:   2020-07-01
tags: [linux, computers]
permalink: /linux/2020-07-01-laptop-fixes 
---

# This page Details issues I have had with my laptop and potential solutions to each of the problems. Both hardware and software issues will be present. 

# Hardware Issues:
# Mic Issues (unsolved)
 For whatever reason, the builtin mic on the xps 9550 is scratchy/ has a lot of background noise to the point where it is unusable. This problem exists on both my Windows and linux so most likely the part will just need to be replace.

# Battery issues (solved)
 When I first bought the laptop from Ebay I had a major issue where the trackpad was not actuating properly. This was rather dishearting at first as I got the laptop for a good deal on ebay and a return was going to be quite a nuasance. With some research it was safe to conclude that the battery had gotten bloated and had to be replace. I bought one from amazon for around 50 dollars [(link)](https://www.amazon.com/Fully-Replacement-Laptop-Battery-Compatible/dp/B07F2GMGWW/ref=sxts_sxwds-bia-wc-p13n1_0?cv_ct_cx=xps+9550+battery&dchild=1&keywords=xps+9550+battery&pd_rd_i=B07F2GMGWW&pd_rd_r=15205205-02d5-453a-963c-9542f4c99d37&pd_rd_w=IzTOJ&pd_rd_wg=Q9A5L&pf_rd_p=1da5beeb-8f71-435c-b5c5-3279a6171294&pf_rd_r=T0T7752WHC34AMH8DEJA&psc=1&qid=1593641850&sr=1-1-70f7c15d-07d8-466a-b325-4be35d7258cc
). It works alright and was easy to replace.

# Software Issues
# Bluetooth Issues: (mostly fixed)
 One of the main issues I have had with my XPS laptop (go to base laptop page for more info) is that the bluetooth on Linux is often quite buggy. I have no doubt that Bluetooth isn't perfect on Linux across all devices but there were various things I had to do to get my bluetooth working.
Main thing was to install an external driver for my particular chip. The [arch wiki](https://wiki.archlinux.org/index.php/Dell_XPS_15_9550) on the xps 9550 makes this quite clear but effectively either install the driver manually or using AUR. Also if you use a journalctl on your bluetooth service you will see something related to goldenhw failing to start. This will typically indicate that you need to install this separate driver. 
This seems to fix most of the problem but I have still had issues where I had to restart my computer several times to fix the bluetooth. In theory, the newest Linux kernel should have this driver already in it but I have still had problems with the default kernel driver before.
	
# Backlight issues - (Fixed)
I had various problems with getting the backlight to work. Instead of messing around with various settings of manually doing it and writing to random text files, I just instead a package [light-git](https://aur.archlinux.org/packages/light-git/) which was easier and has been bullet proof so far.

# Discord Issues (Work around)
Weirdly on this laptop I have discord crash often when in voice all on the desktop client. For the moment, I just use the web client when I need to use the vc. Although, I have had various people tell me that Discord client has been pretty unstable on linux (Manjaro, Ubuntu, Mint).

# Graphics Issues (Work around)
So in my case I have both an integrated GPU and a Discrete GPU. For battery life, I will try to use my integrated gpu as much as possible until I play a game or something. In order to be able to switch gpus I tried a couple of methods.
## Nvidia Optimus 
The [arch wiki]( https://wiki.archlinux.org/index.php/NVIDIA_Optimus ) has a good article on this but effectively optimus will switch between the gpus (or use a hybrid method).
I started out with using the [optimus-manager-qt](https://github.com/Askannz/optimus-manager) however I found customizing it to be a bit annyoing.
The next option (which I am currently using) is the [nvidia-xrun](https://wiki.archlinux.org/index.php/Nvidia-xrun). This is a bit simpler of a program but basically you run this command with an application as an argument and it will turn on the gpu and run the program. Typically, the application is a desktop environment so in my case the command is
{% highlight console %}
nvidia-xrun i3
{% endhighlight %}
This command does have to be run from another console (so using the various CTRL+ALT+Function keys) or you can use a bash script and execute it using your login session. In my case, I have been trying to get this bash method working but to no avail. So for now running it on separate console is the best option.

# DPI/Multi Monitor Configuration (Work-in progress)
Linux's support for multi monitor configurations has always been a bit bad. Some Distro do a better job but overall I am hoping that [wayland](https://wayland.freedesktop.org/) will fix the problems.
For now I have several scripts that solve most of my problems.
[This repo](https://github.com/rommac100/monitor_scripts) contains the various scripts that I used to allow for quicker switches between my laptop and its "dock" setting.
Effectively, I replace the .Xresource file and the i3config and change xrandr settings via the script on long from my login manager (lightdm). In theory, smarter way would to use a compare command and compare the file to be copied and the current file to see if they different to reduce the number of reads and writes (that will be added at some point). There are also some scripts that attempt to enable the Discrete GPU upon login as well but those are not working quite yet (located nvidia/ directory).
*Note currently there is a problem where it requires you to login twice( ie. login, exit, login again) in order to switch properly. This could be fixed somehow but I am unsure of the method as of now. * 

# References
[arch wiki](https://wiki.archlinux.org/index.php/NVIDIA_Optimus)
[optimus-manager-qt](https://github.com/Askannz/optimus-manager)
[nvidia-xrun](https://wiki.archlinux.org/index.php/Nvidia-xrun) 
[wayland](https://wayland.freedesktop.org/)
[switching_scripts_repo](https://github.com/rommac100/monitor_scripts)




