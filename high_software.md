---
title: /high-level-software 
layout: page 
tags: [software]
permalink: /high-software
---

# This page and its sub posts will be dedicate to random high-level software and my various problems and solutions I have had with them. Expect the posts to be "consolidated rambles" with important information mixed in.
# Recent Pages

{% for post in site.posts %}
  <ul>
	{% if post.tags contains "software" %}
	<a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
	{% endif %}
  </ul>
{% endfor %}
