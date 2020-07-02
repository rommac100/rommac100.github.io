---
title: /
layout: default 
permalink: /
---

# Welcome
 This blog will mostly be dedicated to various experiences I have had with electronics based projects. This will range from low-level circuitry and microcontrollers all the way up to Virtual Machines and GPU passthrough. Probably some random misc stuff will exist so just use the top bar to navigate to each category. 

Also expect some grammatical errors here and there as this blog is just meant to convey information rather stream of conscious like. Corrections will occur gradually.

If there is information that you think should be updated. Just submit a pull request on github and I will make the changes. Or use my contact page if necessary.

# Recently Added Pages
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}  -  {{ post.date | slice: 0, 10}}</a>
    </li>
  {% endfor %}
</ul>

