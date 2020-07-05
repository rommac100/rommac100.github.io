---
title: /linux 
layout: page 
tags: [linux, computers]
permalink: /linux
---
# This subpage will be dedicated to everything with regards to Linux (GNU/Linux). 
Linux is an operating system that is typically best known for being particularly lightweight and Open-Source. In my case, it is better for my use cases of low-level software development. It is already heavily used for many other applications (cell phones, enterpise environments - Servers, cars, etc.) but using it on desktops is not entirely common so that is why I will be listing various things I have learned and used since beginning to use it on all of my devices.

*Note* I won't be going into which distro or which DE (Desktop Environment) is the best as that is not entirely important. I will just be discussing the various problems I have had and my solutions or lack of solutions that I have had.


<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Tux-simple.svg/2000px-Tux-simple.svg.png" width="50%" height="50%"/>
# Recent Pages

{% for post in site.posts %}
  <ul>
	{% if post.tags contains "linux" %}
	<a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
	{% endif %}
  </ul>
{% endfor %}
