---
layout: post
title:  "Ebike Page"
date:   2022-01-09 
post_url: /electronics/ebike-page
tags: [electronics]
---
# Synopsis
This page will summarize my ebike and the various phases it has gone through.

# Background
For a long time I have always wanted a motorized bike. So finally when I got a used cargo bike frame for a birthday I decided to go about the conversion.

# Bike Frame
<img src="/_images/electronics/ebike/frame.jpg" width="50%" height="50%" />
 To be honest this bike frame is quite old and the specifics are somewhat unknown. Howevever, I have pieced together this information: Fuji Bike frame (circa pre-2000s) and a Xtracycle Free Radical Cargo Extension (circa pre-2010). These two pieces make this bike incredibly big and unwielding for most people but also makes it by far the most comfortable bike I have ridden assuming you are over 6ft tall (otherwise you won't be able to touch the ground). It is great cruising and the length + cargo extension connection method gives the frame some give when going over bumps which is a great bonus. 

## Frame Problems
Firstly, the frame is made a steel which is good in most cases but can rust so should be monitored ocassionally but not too big of an issue when living in a desert. Secondly, the old frame causes a lot of incompabilites with newer bike parts with regards to anything attaching to the fork. Thirdly, the chain is wieldly long and typically requires at least two off the shelf chain packs when replacing the chain and if not tension properly will bounce around and rub against the frame.. Lastly and the biggest problem, no native disc brakes. I have been wanting solve this problem for a while but effectively I need a fork that most likely does not exist in order to get proper disc brake mounts or find a welder that is willing to attach the mounts to the existing fork. So far this problem has been somewhat mittigated but I would ideally like to still add the disc brakes for greater control sometime in the future. 

## Fork Differences
Effectively, at somepoint threaded forks were deprecated probably sometime in the late 90s to the early 2000s in favor threadless forks. This causes the compatibility problem for my bike in addition to the steering tube needing to be unearthly lon.g

# E-Bike V1
With the long chain problem in mind, I decided to go with a rear hub motor wheel as the main motor source for my ebike. Now a days a lot of people prefer a type of motor called mid-drive with effectively integrates with your pedals/crank arms and powers the rear using the chain. This has the advantage of being able to use your existing gearing which is great for efficiencies. Unfortunately, I don't trust my chain to hold up against that sort of wear while also being incredibly long so the older hub motor method was preferred. These older hubs are typically just less efficient but are typically more durable (although I would not say this to be exactly true in my case).

# Mechnical Changes
Since the original bike was used when purchased a lot of mechanical parts had to be replaced. Specifically, but shifters were effectively worn out, all mechanical cable lines needed to be replaced, and brake pads needed to be replaced. This was done and was a semi costly since I needed two non standard length brake and shifting lines due to the sheer length of the bike. I also cheaped out on the shifters which was a bad mistake so I don't recommend going with the ones I bought. Just buy some used or brand new genuine Schimano or nicer brand shifters and you should be fine.

## Motor Kit Purchased
The motor kit I used was the typical ~$200 [Voilamart Rear Hub kit](https://www.ebay.com/itm/Voilamart-Electric-Bicycle-E-Bike-26-Front-Rear-Wheel-Motor-Conversion-Kit/322247604604). It can come with a rudimentary LCD or not but comes with all the parts with exception of the battery to perform an ebike conversion. This motor kit is incredibly cheap (which will cause issues later on) but worked decently for the V1 bike. Additionally, the installation process was pretty straight forward and could technically be done with only rudimentry hand tools but I would highly recommend at least having a soldering iron to shorten some wires for a cleaner setup.

*Important note*
The motor + freewheel is quite wide and may cause incompatibilites with your frame. Despite the overall size of my frame I still couldn't use all 7 of the rear gears.

## Battery Purchased
This was by far the biggest annoyance with the V1 E-Bike. I first picked up a very cheap 48v 20ah ebike battery from an ebay seller (won't link since it was a waste of money) and technically the bike could move with that motor but I would always trip the BMS on the battery for over current. This obviously was not correct so I managed to contact the seller and return the battery. My next battery which was substantially better was Unit Pack Power Battery.
<img src="/_images/electronics/ebike/upp_bat.jpg" width="50%" height="50%" />
This battery was also a 48v 20ah battery and did perform as expected but DO NOT GET THIS BATTERY. Some models from this seller have been known to catch on fire (specifically their no longer sold 72v batteries) so I do not recommend going with this battery at all despite it working just fine for me.

## Finally Completed V1 Ebike
<img src="/_images/electronics/ebike/bikev1.jpg" width="50%" height="50%" />
Despite the problems faced, this first version was too much fun and turned out very nice and clean (unfortunately never looks as clean again). When riding around in Hilly California I got great range despite my size and the size of the bike (approx. 30 miles of range while pedaling). My only recommendation if you were to repeat this v1 exactly would be to get the motor kit with the LCD so that your Pedal Assist ratio (motor:human ratio) could be adjusted.


# Resources:
 - [ASRock C2750D4I Page](https://www.asrockrack.com/general/productdetail.asp?Model=C2750D4I#Manual)
 - [ASrock C2550D4I Page](https://www.asrockrack.com/general/productdetail.asp?Model=C2550D4I#Specifications)
 - [Form post on various attempts/fixes for clock decay](https://www.truenas.com/community/threads/how-to-fix-asrock-c2750d4i-with-c2000-bug.90451/)
 - [Article on the C2000 Atom Clock Decay problem](https://www.extremetech.com/computing/244074-intel-atom-c2000-bug-killing-products-multiple-manufacturers)
