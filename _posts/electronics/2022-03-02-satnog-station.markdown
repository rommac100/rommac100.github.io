---
layout: post
title:  "Satnog Satellite Ground Station"
date:   2022-03-02 
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

# Antenna Selection
Since I didn't want a rotor based Antenna and need an omnidirectional radiation pattern, I decided to try using a Lindenblad antenna for the UHF band. Specifically, I utilize this [design](https://www.thingiverse.com/thing:4626749) which is a revision of a parasitic variant of the Lindenblad Antenna. The advantage of this lindenblad antenna over more traditional ones is that there is only 1 driven element and the rest are passive (read more on the original lindenblad design if desired).

## Elevation Plot
<img src="/_images/electronics/satnog/elev.png" width="50%" height="50%" />

## Azimuth Plot
<img src="/_images/electronics/satnog/azi.png" width="50%" height="50%" />

With those above plots, it is quite clear that a omnidirectional radiation pattern was produced, although the elevation plot is bit gross but is still relatively sufficient and better than a simple dipole.

# Deployment of the Antenna
Since I decided to use the 3D printed variant of the parasitic Lindenblad antenna, I printed out and built a Steel Variant of it.
## Steel Variant Antenna
<img src="/_images/electronics/satnog/steel_lindenblad.jpg" width="50%" height="50%"/>
This Steel Variant technically worked but was not ideal bc of the material selection (low conductivity, can rust, etc). So a second attempt at making the antenna was made using the original aluminum plans.

## Aluminum Variant Antenna
<img src="/_images/electronics/satnog/alum_lindenblad.jpg" width="50%" height="50%"/>
Once probably tuned I managed to get the VSWR down to a max of 1.5 in the 70cm band. Not great but a lot better than before.

## VSWR/Return Loss Plot over 70cm band
<img src="/_images/electronics/satnog/vswr_alumn.png" width="50%" height="50%"/>

# Resources:
 - [Satnog Website](https://satnogs.org)
 - [Lindenblad 70cm Antenna Design](https://www.amsat.org/wordpress/wp-content/uploads/2014/01/70ParaLindy.pdf)
 - [Lindenblad 3D printed revision](https://www.thingiverse.com/thing:4626749)
