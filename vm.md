---
title: /vm 
layout: page
permalink: /vm
---
# This subpage will be dedicated to everything with regards to QEMU and VMs. 

Effectively, this subpage will have various links and posts on how I have setup various VMs for odd ball things (GPU passthrough, iGVT, Development Environment, Sandboxes).
Also for anyone just understanding what vms are:
	Virtual Machines (VMs) are as they are spelled. Virtual Computers are Computers within computers that either use physical hardware or virtualized hardware for dedicated tasks. In the enterprise world, VMs are used in many scenarios where it is preferable to have one computer that contains many mini computers for separate tasks. For many consumers, VMs are used in order to run one operating system at the same time as another. Some common ones are, Hyper-V, Parallels, and VMware. Particularly recently, many linux users have begun using VMs in order to play Windows Video Games that have not gotten a native or semi-native port as dedicated Hardware Passthrough (i.e having VMs use physical hardware instead of simulate hardware) has gotten better and easier to do without using paid software. 
There is obviously a lot more to describe but other articles do a better job at explained the uses for VMs and the types.
Recent Posts:
{% for post in site.posts %}
  <ul>
	{% if post.tags contains "vm" %}
	<a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
	{% endif %}
  </ul>
{% endfor %}
