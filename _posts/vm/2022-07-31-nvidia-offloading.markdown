---
layout: post
title:  "Nvidia Offloading"
date:   2022-07-31 
tags: [computer, vm, passthrough]
---
# Synopsis
If you are interested in utilizing your Nvidia GPU/primary gpu while also passing it through occasionally, I suggest you look at the scripts present in this guide. They can be used to unbind and bind a nvidia gpu successfully. Note you should only run these when your x11 or wayland session is not running.

# Libvirt Hooks
Effectively just follow this guide for setting up hooks and your problems should be resolved. Make sure your gpu is bound to vfio on boot though either via kernel parameters or some other means. [bryansteiner-guide](https://github.com/bryansteiner/gpu-passthrough-tutorial)

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
