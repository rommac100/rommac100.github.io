---
layout: post
title:  "Supermicro Server"
date:   2021-10-03
tags: [linux, computers, servers]
post_url: /linux/2021-10-03-supermicro-server
---
# Summary
 This article just details my supermicro server and contains useful links/information for other people and for personal usage.

# IPMI stuff
 - Default Information: ADMIN,ADMIN



## Remote Console:
 - For Linux users, check out this guide which helps with getting it working underneath linux.
   - [Remote Console](https://forums.servethehome.com/index.php?threads/psa-fix-supermicro-no-ikvm64-in-java-library-path.32302/)

## Power Management:
 - In case you turn off your server for power saving purposes (i.e peak power mitigation), the following commands would probably be helpful. Assuming you have someway to trigger them separately (rpi, constantly running server, etc).
<a/>
Turn on:
``` bash
ipmitool -I lanplus -H (server ip or hostname) -U (username for ipmi) -P (password for ipmi) chassis power on
```
<a/>
For Safe turn off (properly shutdowns OS - not hard shutdown)
```bash
ipmitool -I lanplus -H (server ip or hostname) -U (username for ipmi) -P (password for ipmi) chassis power soft
```

# Resources
 - [9211-8i Guide](https://nguvu.org/freenas/Convert-LSI-HBA-card-to-IT-mode/)
 - [LSI firmware download page](https://www.broadcom.com/support/download-search)
