---
layout: post
title:  "Nvidia Offloading"
date:   2022-07-31 
tags: [computer, vm, passthrough]
---
# Synopsis
If you are interested in utilizing your Nvidia GPU/primary gpu while also passing it through occasionally, I suggest you look at the scripts present in this guide. They can be used to unbind and bind a nvidia gpu successfully. Note you should only run these when your x11 or wayland session is not running.

# Binding nvidia scripts
## bind_nvidia script
Note replace pci address as needed for both the nvidia gpu and the audio device.
```bash
#!/bin/bash

echo -n "0000:0b:00.1" > /sys/bus/pci/drivers/vfio-pci/unbind
echo -n "0000:0b:00.0" > /sys/bus/pci/drivers/vfio-pci/unbind

echo -n "0000:0b:00.1" > /sys/bus/pci/drivers/snd_hda_intel/bind
echo -n "0000:0b:00.0" > /sys/bus/pci/drivers/nvidia/bind
```

## unbind_nvidia script
Note replace pci address as needed for both the nvidia gpu and the audio device.
```bash
#!/bin/bash

echo -n "0000:0b:00.1" > /sys/bus/pci/drivers/snd_hda_intel/unbind
echo -n "0000:0b:00.0" > /sys/bus/pci/drivers/nvidia/unbind
```

I don't recommend using this method binding the vfio driver instead I recommend doing that with a libvirt hook:

# Libvirt Hooks
Firstly, follow this github guide on setting up the hooks (additionally a helpful/useful reference for settings 3900x based gpu passthrough setup) [bryansteiner-guide](https://github.com/bryansteiner/gpu-passthrough-tutorial)
## libvirt hook prepare/begin
```bash
#!/bin/bash

## Load the config file
source "/etc/libvirt/hooks/kvm.conf"

# Unload Nvidia drivers
#modprobe -r nvidia
#modprobe -r nvidia_drm

## Load vfio
modprobe vfio
modprobe vfio_iommu_type1
modprobe vfio_pci


## Unbind gpu from nvidia and bind to vfio
virsh nodedev-reattach $VIRSH_GPU_VIDEO
virsh nodedev-reattach $VIRSH_GPU_AUDIO
```

## libvirt hook release/end
```bash
#!/bin/bash

## Load the config file
source "/etc/libvirt/hooks/kvm.conf"

# Load Nvidia drivers
modprobe nvidia
modprobe nvidia_drm
```


# Have applications use that specific gpu.
I used nvidia prime to do this operation (which works in sway additionally) but effectively install the [nvidia-prime](https://archlinux.org/packages/extra/any/nvidia-prime/) package.
<a/>
Then use the following syntax to run the application with a different gpu as a renderer
```bash
prime-run <application>
```

# Related Posts:
{% for post in site.posts %}
  <ul>
	{% if post.tags contains "passthrough" %}
	<a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
	{% endif %}
  </ul>
{% endfor %}


# References:
 - [https://www.qemu.org/](https://www.qemu.org/)
 - [bryansteiner-guide](https://github.com/bryansteiner/gpu-passthrough-tutorial)
 - [https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF)
