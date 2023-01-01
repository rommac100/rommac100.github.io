---
layout: post
title:  "GPU Passthrough issues"
date:   2020-07-01 
tags: [computer, vm, passthrough]
---
# This page details the various issues that I have had to over come with GPU Passthrough.

## Code 43 Error (Solved):
This error occurs for Nvidia GPUs when you attempt to pass them through and they are not Quadros gpu. Effectively
Nvidia does not appreciate when you try to use a Gefore based video card for VMs. Thankfully this is an easy fix.

If you are using libvirtd: Use virsh and edit your VM's base configuration file. Look for the hyperv and insert the following code: 
{% highlight xml %}
<vendor_id state='on' value='whatever'/>
{% endhighlight %}
Then above the end of the features xml category insert the following code:

{% highlight xml %}
<kvm>
	<hidden state='on'/>
</kvm>
{% endhighlight %}

These pieces of code will effectively trick the nvidia driver (which causing the problem) and should allow for full functionality of passthroughed gpu.

*Note* There is a chance that your gpu is missing a uefi bios and that could also be causing the issue. Look on the [arch wiki]( https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF) for more details.

## Audio Issues
Quite frankly audio issues are pain to deal with. I have setup gpu passthrough for several different machines and there really isn't a "one size fits all" solution.

With my limited sample size (of roughly 3 machines), I have had  success using audio "passthrough" via pulseaudio and Screen Audio streaming.

# Pulseaudio passthrough
In order to start using it, there are several different files you will have to edit, your qemu.conf file, and your vm's xml config file.

Beginning with the qemu.conf (needed so that pulseaudio can have the correct permissions to work with qemu).
{% highlight console %}
/etc/libvirt/qemu.conf
user = "example"

{% endhighlight %}
Effectively, find the above line and uncomment it (remove pound symbol) and change example to your linux username.

Next change to editing your vm xml file using virsh
{% highlight console %}
virsh edit [vmname]
<domain type='kvm'>
{% endhighlight %}
Change the above line to:
{% highlight console %}
virsh edit [vmname]
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>
{% endhighlight %}

Then navigate to the closing devices tag and insert the following code
{% highlight console %}
<qemu:commandline>
        <qemu:arg value="-audiodev"/>
        <qemu:arg value="pa,id=snd0,server=/run/user/1000/pulse/native"/>
</qemu:commandline>
{% endhighlight %}

The above changes should get audio working for the most part and are tested to a certain extent. 
*Note* Recently in QEMU 4.0/4.2 there have been some new audio changes that have improve pulseaudio passthrough. I haven't tested them but Arch wiki discuss what is necessary. I will added them to this guide once they have been tested.

# Identical Vendor IDs
 Since virtio requires vendor ids in order to properly passthrough, two or more gpus with identical ids posses a problem. The Arch wiki on gpu passthrough (the gospel at this point) does provide a solution by adding a script that manually binds gpus to the virtio driver via a pci address (like 0000:00:02.0). However, this guide does not perfectly translate to other distros where mkinitcpio is present (which in this solution is somewhat necessary in order to bind early enough). I have yet to test a way to do it on other distros but I can confirm that this solution does work on the one system where it was necessary. Will update once I have tested it on at least debian.

# Incorrect Resolution For Linux with Virtio.
 More or less just use this article for a basis to fix this issue. Not strictly a gpu passthrough related issue but still relevant to VMs.
 [high res vm guide](https://stafwag.github.io/blog/blog/2018/04/22/high-screen-resolution-on-a-kvm-virtual-machine-with-qxl/)
 1. Make sure your specified VM gpu memory is correct for the resolution desired. i.e high enough.
 2. Use xrandr to get the right modeline config.
 3. Add the modeline config to your screen config

## For 2560x1440_60.00 Steps - Scrapped from the guide
1. Video Ram Calculations for 1440p
<a/>
```bash
2560x1440 = 3686400
3686400x32=265420800, /8 = 14745600
14745600/(1024*1024) = 14.0625M. (round up to the nearest 2 power).
```
<a/>
so as long as the video memory is at least 16MB this resolution is doable. Otherwise update your libvirt config
2. Use Xrandr to get the right modeline config.
<a/>
xrandr output:
```bash
Screen 0: minimum 320 x 200, current 1280 x 800, maximum 8192 x 8192
Virtual-1 connected primary 1280x800+0+0 (normal left inverted right x axis y axis) 325mm x 203mm
   1280x800      74.99*+
   5120x2160     50.00  
   4096x2160     50.00  
   3840x2160     60.00    50.00    59.94  
   1920x1440     60.00  
   2560x1080     50.00  
   1856x1392     60.00  
   1792x1344     60.00  
   2048x1152     60.00  
   1920x1200     59.88  
   1920x1080     60.00    50.00  
   1600x1200     60.00  
   1680x1050     59.95  
   1400x1050     59.98  
   1280x1024     60.02  
   1440x900      59.89  
   1280x960      60.00  
   1360x768      60.02  
   1280x768      59.87  
   1024x768      60.00  
   800x600       60.32  
   640x480       60.00    59.94  
```
<a/>
So screen is screen 0 with Virtual-1 as the primary display.
Now use cvt to get the modeline.
<a/>
```bash
$cvt 2560 1440 
# 2560x1440 59.96 Hz (CVT 3.69M9) hsync: 89.52 kHz; pclk: 312.25 MHz
Modeline "2560x1440_60.00"  312.25  2560 2752 3024 3488  1440 1443 1448 1493 -hsync +vsync
```
<a/>
3. Create and add modeline
```bash
$xrandr --newmode "2560x1440_60.00"  312.25  2560 2752 3024 3488  1440 1443 1448 1493 -hsync +vsync
$xrandr --addmode Virtual-1 2560x1440_60.00
```
Now at this point the different resolution can be selected via xrandr or your normal display setting on linux (whatever your distro does more or less, arandr, gnome-control-center, etc).


## References:
 - [https://www.qemu.org/](https://www.qemu.org/)
 - [https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF)
 - [high res vm guide](https://stafwag.github.io/blog/blog/2018/04/22/high-screen-resolution-on-a-kvm-virtual-machine-with-qxl/)
