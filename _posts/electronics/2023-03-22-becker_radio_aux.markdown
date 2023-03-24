---
layout: post
title:  "Becker 612 Radio Aux Mod"
date:   2023-03-22
post_url: /electronics/becker-aux
tags: [electronics]
---
# Synopsis
This page will summarize the quick and dirty mod of adding an aux cord to the Becker 612 Radio. This radio is from a 1984 W126 Mercedes but that isn't terribly relevent. I suspect though this mod can be done to many other becker radios if you are a little clever about it. 

# Disassembly Process
I will assume the radio has been removed already from the car but you will see 3 metal bent flaps that need to pull away from the chassis. Once this is done the two large panels can be pulled away from the radio. Otherwise reference this [guide](http://madrona.ca/e/radio/BeckerGP612/index.html) which is pretty informative. We are specifcally interest in the top of the radio which has the ic that we want to insert our signal.

# Mod Summary
Basically after searching throughout peachparts forums and other car forums I found a couple rough guides on adding aux. Most involved using some features of the tape deck (not terribly useful if your tape deck is broken) but the last post I found talked about just inserting your line level signal (3.5mm aux signal typically is this) directly to the output of a stereo decoder chip. In the guide for becker 1432 radio this IC is a TCA 4511. For the Becker 612 this IC is a [TCA4500](https://datasheetspdf.com/pdf-file/552312/ETC/TCA4500A/1). Basically just solder your aux aux cord to the pins 4,5,8 (L,R,G) and you should be good to go.
<img src="/_images/electronics/becker/mod.jpg"/>

# Current Issues
 - There is a loud poping noise that occurs when switching sources (pretty typical of sound stuff) but I am unsure of how to fix it.
<a/>
 - The cord just comes out through the cassette so not terribly clean but this can be routed differently.
<a/>
 - The point where soldered may not be ideal in terms of filtering and stuff. Should be checked later especially if schematic is obtained somewhere

# Resources:
 - [TCA4500 Datasheet](https://datasheetspdf.com/pdf-file/552312/ETC/TCA4500A/1)
