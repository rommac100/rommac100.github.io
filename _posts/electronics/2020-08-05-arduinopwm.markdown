---
layout: post
title:  "Arduino PWM Testing"
date:   2020-08-05 
post_url: /electronics/arduino-pwm
tags: [electronics]
---
# Synopsis
In my first pwm related article I go a bit more in detail regarding the theory of pwm and how it works [RISC-V PWM Testing]({{ '/electronics/riscv-pwm' | relative_url }}). In summary, pwm is a way to a cheap analog voltage using digital signals by periodically switching between Vcc and Vss. In my case, I tend to use pwm to simulate clocks since many digital devices are capable of deciphering that the "analog voltage" coming from the pwm signal is not analog voltage. Regardless, the setup to output an pwm signal is a bit more straight forward on AVR base devices.

# Setup
For the purposes of my Z80 project, I ended up using attiny85 as I needed vary few digital pins and a small package size (as my bread board was getting rather full at this point with the large number of ICs that were present).
<img src="/_images/electronics/z80/attiny85_pinout.png" width="80%" height="80%"/>

# Helpful Resources:
- [Attiny85 Datasheet](http://www.farnell.com/datasheets/1698186.pdf#G1.2000842)
- [Reset/PWM generator repo]()

# Sibling Posts
- [Base Z80 Project]({{ '/electronics/z80_proj' | relative_url }})
- [RISC-V PWM Testing]({{ '/electronics/riscv-pwm' | relative_url }})
