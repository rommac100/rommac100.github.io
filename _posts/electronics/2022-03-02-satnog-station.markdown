---
layout: post
title:  "Satnog Satellite Ground Station"
date:   2022-01-09 
post_url: /electronics/satnog
tags: [electronics]
---
# Synopsis
This page will summarize my work in progress Satnog ground station.

# Background
I work in CubeSat lab at ASU so I got introduced to the Satnog ground station network and got interested in setting one up at my apartment. Obviously, I couldn't setup a rotor based antenna on my porch, so I decided to try out an Omnidirectional Stationary Antenna. 

# Satnog
More or less satnog is a easy to use ground station network where you put your ground station live and start reporting your results. Makes it easier to track satellites and also track satellites over time to see which ones are still responsive as most satellites (especially cubesats) are not the best at reporting information pertaining to their satellite after launch.
<a/>
I recommend if you wish to give involved in Satnogs stuff to continue reading this article and also check out their [website](https://satnogs.org) as they have stream line the process heavily.
<a/>
More or less a typical satnog ground station will consist of an Antenna (either stationary or rotor based), a LNA (Low Noise Amplifier), a RTL-SDR software defined radio as the receiver and a Raspberry Pi (3 or 4) with a satnog image to act as the ground station computer.

# Resources:
 - [Satnog Website](https://satnogs.org)
 - [Lindenblad 70cm Antenna Design](https://www.amsat.org/wordpress/wp-content/uploads/2014/01/70ParaLindy.pdf)
 - [Lindenblad 3D printed revision](https://www.thingiverse.com/thing:4626749)
