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


## References:
 - [https://www.qemu.org/](https://www.qemu.org/)
 - [https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF)
