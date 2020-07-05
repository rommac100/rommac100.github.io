---
title: /electronics 
layout: page
permalink: /electronics
tags: [electronics]
---
# This subpage will be dedicated to everything with regards to micro-electronics. 

<img src="https://www.electronics-tutorials.ws/wp-content/uploads/2018/05/waveforms-tim37.gif" width="50%" height="50%"/>

Recent Posts:
{% for post in site.posts %}
  <ul>
	{% if post.tags contains "electronics" %}
	<a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
	{% endif %}
  </ul>
{% endfor %}
