---
title: /linux 
layout: page 
tags: [linux, computers]
permalink: /linux
---
# This subpage will be dedicated to everything with regards to Linux (GNU/Linux). 

# Recent Pages

{% for post in site.posts %}
  <ul>
	{% if post.tags contains "linux" %}
	<a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
	{% endif %}
  </ul>
{% endfor %}
