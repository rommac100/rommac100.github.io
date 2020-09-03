---
layout: post
title:  "GPU Stacked DVI Converter"
date:   2020-08-23 
post_url: /electronics/dvi-converter
tags: [electronics]
---
# Synopsis
The goal of this adapter is to convert the stacked DVI connector (i.e two dvi connections vertically on top of each other) that is common on gpus to two hdmi connectors that are horizontally positioned.
** Stacked DVI Connector **
<img src="https://c1.neweggimages.com/NeweggImage/ProductImageCompressAll1280/14-487-075_R01.jpg" width="90%" height="90%"/>

# Removing Old Connector
While I was waiting for the pcb to arrive/while I was designing, I started the process of removing the connector from the gpu. 
I first attempted to using a solder sucker and a quality solder iron, this turned out to be a bad decision due the multi layer design of basically all gpus (too much heat is required and too easy to disipate the heat). This basically meant that sucking would never work properly. I also tried using solder wick but I found it to not work not that great either (though I could be just a novice at using solder wick as I only recently started using it after finding a brand that was not horrible).
<a/>
* Solution *
Basically, the solution was to get a cheap heatgun and use that to remove the connector. I ended up getting one of these on amazon (effectively a hakko 858d rip off):
<img src="https://images-na.ssl-images-amazon.com/images/I/71P9XekiKXL._AC_SL1500_.jpg" width="90%" height="90%"/>
These cheap rework stations can be quite handy though some have been known for being dangerously miswired so always open them up and check the wiring before proceeding to use it [eevblog](https://www.eevblog.com/forum/chat/deadly-wiring-fault-atten-858d-hot-air-rework-station/).
Once this arrived, I simply heated all of the pins and was able to remove the connector off of the gpu (note a decent amount of rocking motion about the connector was needed using pliers but this may not be necessary if you have a better smd rework station or a better technique).
<img src="/_images/electronics/gpu_mods/remove_dvi.jpg" width="90%" height="90%" />
# Helpful Resources:
- [SMD Rework Station](https://www.amazon.com/gp/product/B01MR2IWBN/ref=ppx_yo_dt_b_asin_title_o05_s00?ie=UTF8&psc=1)


# Sibling Posts
