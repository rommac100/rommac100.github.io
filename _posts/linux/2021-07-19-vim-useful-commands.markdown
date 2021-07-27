---
layout: post
title:  "Useful Vim Commands"
date:   2021-07-19
tags: [linux, computers]
post_url: /linux/2021-07-19-useful-vim-commands
---
# Summary
 This article will be summarizing several different useful vim commands. Basically a reference page in case you need some random esoteric vim command and don't want to go through stack over flow.


# Basic Stuff
 Adding to the end of a line - Shift + A
<a/>
 Send cursor to previous position - CTRL + o
<a/>
 Scrolling up and down - CTRL + u , CTRL + d

# Incrementing array indexes
 Lets say you copy a c array addressing many times and which to increment the index i.e
```c
ind[0] = 1;

ind[0]= 1;
ind[0]= 1;
ind[0]= 1;
ind[0]= 1;
ind[0]= 1;
ind[0]= 1;
```
So that into this:
```c
ind[0] = 1;

ind[1]= 1;
ind[2]= 1;
ind[3]= 1;
ind[4]= 1;
ind[5]= 1;
ind[6]= 1;
```
The sequence of commands consists of visual block over the indexes and then g+CTRL+a





# Resources
 - [Vim Manuals](https://www.vim.org/docs.php)
