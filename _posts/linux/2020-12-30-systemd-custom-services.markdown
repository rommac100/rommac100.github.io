---
layout: post
title:  "Custom Linux Services"
date:   2020-12-30
tags: [linux, computers]
post_url: /linux/2020-12-30-custom-linux-services
---
# Summary
This article will summarize the basics for creating services in linux. Some parts will work on all Linux distros and others will be specific to Arch Linux. So take the article with a grain of salt. 

Also the reason for creating a service in general is to have a program/script/application/etc start automatically and run in the background. 

# Basics
 A .service file consists of three parts more or less: [Unit], [Service], [Install]. 
<a/>
The **Unit** section contains a general description of the service (i.e you should describe what the service will do) the order in launching (i.e start after networking or some other task). There are plenty of other options to add to the Unit but those two are the most crucial.
<a/>
The **Service** section describe a bit regarding the actual operation of the service. In most cases, you will describe the type of service that it is (see resources for the man article on the various options). If you are just launching a simple onetime script, the option "simple" should work just fine, or "oneshot" should work fine.
*Note depending on the type selected, you will have add to the restart options as well, but the Man article does a decent job describing it.*
The next critical parameter, is which user should be executing the script. This entirely will depend on your application and what permissions are needed. For my test application, the root user had to be used. The last necessary parameters it the "ExecStart" parameter which is where you would specify your script, or application that you wish to run.

<a/>
In the **Install** section, the only main option that is required is the "WantedBy" option. In most cases, the "multi-user.target" parameter will work fine.


# Example service
```bash
[Unit]
Description=Sets CPU governor to performance.
After=network.target

[Service]
Type=oneshot
User=root
ExecStart=/usr/bin/bash /home/rommac/.scripts/cpu_performance.sh

[Install]
WantedBy=multi-user.target
```





# Resources
 - [Man Article on Systemd and .Services](https://man7.org/linux/man-pages/man5/systemd.service.5.html)
