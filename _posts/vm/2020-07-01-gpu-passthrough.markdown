---
layout: post
title:  "GPU Passthrough"
date:   2020-07-01 
tags: [computer, vm, passthrough]
---
# Synopsis
 Effectively, GPU passthrough is a form of direct hardware passthrough or utilization to a given VM. The technology has been availble for quite a while in the enterpise sector but only recently did free/open source version began to exist.
For most people, [QEMU](https://www.qemu.org/) should be used (especially if you are on Linux) for GPU passthrough as it has the best support for it at the moment and is the main open source Virtual Machine available on linux. For the purposes of the blog, I will be mostly looking at GPU passthrough for its uses in gaming but you can use GPU passthrough and in general direct hardware passthrough for many applications.

# Outline of the Process
	- Verification of Hardware Compatibility
	- Pick Variant of GPU passthrough.
	- Prepare machine for Passthrough.
	- Prepare VM for passthrough.
	- Tune.
	- Enjoy! 

The above outline should give a general idea of what you will have to do in order to get GPU passthrough working. For some machines it will be super simple, others not so much.

Regardless of what distro you use, I highly suggest you look at the [Arch Wiki](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF) as I will be referencing it heavily and it has best guide at the moment (beyond this one).

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
 - [https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF)


