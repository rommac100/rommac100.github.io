---
title: /electronics 
layout: page
permalink: /electronics
tags: [electronics]
---
# This subpage will be dedicated to everything with regards to micro-electronics. 

Recent Posts:
{% for post in site.posts %}
  <ul>
	{% if post.tags contains "electronics" %}
	<a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
	{% endif %}
  </ul>
{% endfor %}
