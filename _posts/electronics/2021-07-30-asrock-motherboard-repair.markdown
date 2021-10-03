---
layout: post
title:  "Asrock Motherboard Repair"
date:   2021-07-30 
post_url: /electronics/asrock-motherboard-repair
tags: [electronics]
---
# Synopsis
 This article will be describing some of the repairs that I have performed on the Asrock C2550D4i and C2750D4i. Mostly involving cloning bios chips, bmc chips and some kludges involving pulling clock signals high.

# Background
 So I have always been semi fond of the Asrock Avoton series of motherboards. They are pretty old as 2021 but they have some decent features (12 sata ports, dual gig ethernet and up to 64GB of memory). All in itx form factor. Unfortunately, these boards have not aged great and have several flaws associated with them. 
<img src= "https://www.asrockrack.com/photo/C2750D4I-1(L).jpg" width="50%" height="50%"/>

# Flaws
 - PCICLK Decay
 - BMC Chip Decay
 - Broadcom Sata Controller Bugs.

# PCICLK Decay
 This isn't inheritanly an asrock problem but more of an Intel Atom problem that was associated with the avoton series where eventually the PCIClk (note this is the clock name on the TPM connector and may be the incorrect term) eventually decays and no longer functions correctly.
 Althou

# Resources:
 - [ASRock C2750D4I Page](https://www.asrockrack.com/general/productdetail.asp?Model=C2750D4I#Manual)
 - [ASrock C2550D4I Page](https://www.asrockrack.com/general/productdetail.asp?Model=C2550D4I#Specifications)
 - [Form post on various attempts/fixes for clock decay](https://www.truenas.com/community/threads/how-to-fix-asrock-c2750d4i-with-c2000-bug.90451/)
 - [Article on the C2000 Atom Clock Decay problem](https://www.extremetech.com/computing/244074-intel-atom-c2000-bug-killing-products-multiple-manufacturers)
