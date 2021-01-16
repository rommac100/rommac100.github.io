---
layout: post
title:  "Portforwarding Plex through PIA"
date:   2021-01-12
tags: [linux, computers]
post_url: /linux/2021-01-12-pia-portforward
---
# Summary
 This article will summarize the setup process of port forwarding with Plex and Private Internet Access. The whole purpose of this is if you want to watch plex remotely but are blocked by Carrier Grade NATs (i.e cannot use traditional port forwarding methods).

# Grabbing PIA's repo and setting up
 PIA (private internet access) thankfully puts out a [github repo](https://github.com/pia-foss/manual-connections#dependencies) that automates the process of port forwarding. Basically, clone the repo and run the run_setup.sh script (make sure you have all of the dependencies though installed).
<a/>
 If you have all of the dependencies installed, you should encounter several prompts regarding how you want the vpn setup. 
Enter your username and password for PIA, and then choose the options that you want out of the prompts that are given. I personally setup my with the following options: 
<a/> Openvpn=Y <a/>  UDP=Y <a/> Strong Encryption=N <a/> Force PIA DNS=N <a/> Forwarding Port Assigned = Y <a/> Latency=50ms <a/> Disable IPv6 = Y<a/> 
Once you have finished the prompts, a bunch of info will be spat out, the main things to note are the VPN IP address and the PIA port.
 Put this port into plex's Port Forward section, and you should be able to now access your plex server externally. *Note the port expires/ needs to be renewed every 60 days*

# Optimizing this for plex setup
 So in my case, I couldn't get plex to accept this port when using their manual port selection option. Instead I used a nginx reverse proxy setup. *Note this will make your plex connection insecure unless you feel like setting up https (which is out of the scope of this brief guide*
<a/>
Firstly, I made a couple of scripts that make the pia scripts work without console prompts (more or less just sets the key environment variables).

# Connect to server and enable port forwarding script
*Note that you will want to change the cd directory so that it matches the root directory of your pia cloned repo*
"connect_vpn.sh"
``` bash
#!/bin/bash
# takens a specified token and starts grabbing stuff.
cd /home/theatre/.scripts/manual-connections

if [ $1 = "-k" ]; then
        echo Killing VPN
        kill `cat kill_id`
        exit
else
        export PIA_USER=xxxx
        export PIA_PASS=xxxx
        export PIA_PF=true
        export PIA_AUTOCONNECT=openvpn_udp_standard
        /bin/bash /home/theatre/.scripts/manual-connections/get_region_and_token.sh
fi
```
Obviously, you should isnert your private internet access username and password where applicable.

# Nginx Reverse proxy setup
So I just have a very simple reverse proxy setup in nginx which just takes the given pia port and forwards the traffic from the plex server. Replace the parameters *proxy_pass* and *listen* with the appropiate values (i.e correct local ip address for pia and the correct pia vpn port).
<a/>
"nginx.conf"
``` bash
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
        worker_connections 768;
        # multi_accept on;
}

http {

  server {
    listen 26557;
    location /{
      proxy_pass http://192.168.12.8:32400;
    }
  }
        ##
        # Basic Settings
        ##

        sendfile on;
        tcp_nopush on;
        tcp_nodelay on;
        keepalive_timeout 65;
        types_hash_max_size 2048;
        # server_tokens off;

        # server_names_hash_bucket_size 64;
        # server_name_in_redirect off;

        include /etc/nginx/mime.types;
        default_type application/octet-stream;

        ##
        # SSL Settings
        ##

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE
        ssl_prefer_server_ciphers on;

        ##
        # Logging Settings
        ##

        access_log /var/log/nginx/access.log;
        error_log /var/log/nginx/error.log;

        ##
        # Gzip Settings
        ##

        gzip on;

        # gzip_vary on;
        # gzip_proxied any;
        # gzip_comp_level 6;
        # gzip_buffers 16 8k;
        # gzip_http_version 1.1;
        # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

        ##
        # Virtual Host Configs
        ##

        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
}
```
At this point, the setup should be working and you should be able to access your plex server remotely without bandwidth limitations.

# Automating the setup with Systemd
If the server were to stop at any point, you would have restart the pia portforwarding, the vpn connection, and update the nginx port. This is obviously time consuming, so setting up some basic systemd services will allow the setup to be fully automated (with the exception of grabbing the port and public ip for external use as this obviously cannot really be automated).

# Modifying the pia repo
There are a couple changes that need to be done to get this automation working. Firstly, we need to store the pia port somewhere so that the nginx port can be updated. Secondly, the session id needs to stored so that the vpn connection can be killed properly via systemd. In both cases, I just export the numbers to two files (and delete those files when the scripts are started). 
<a/>
For storing the port, edit the port_forwarding.sh script and add and echo line just after when the port is created.
"port_forwarding.sh"
``` bash
Trying to bind the port..."
rm port_pia
echo $port >> port_pia
```
<a/>
For storing the session id/process id, edit the connect_to_openvpn_with_token.sh script and add this just after the "--> sudo kill $ovpn_pid <--" line.
"connect_to_openvpn_with_token.sh"
```bash
rm kill_id
echo $ovpn_pid >> kill_id
```

With these changes, we can make one more script which will make the appropriate changes to nginx whenever the port has been updated.
"nginx_update.sh"
```bash
#!/bin/bash
cd /home/theatre/.scripts/manual-connections
port=$(cat port_pia)
sed -i "s/listen .*$/listen ${port};/g" /etc/nginx/nginx.conf
systemctl restart nginx
```
Again change the cd directory to match your pia cloned repo directory.

# Adding Systemd scripts
Since these scipts have to start with a bit of a time gap (as the initial vpn connection takes a bit of time so the port and session id files won't be updated yet), I have the second script start with a 30 second delay. Also a systemd target is used to "tie" these two services together. See my other guide on systemd if you need a basic intro. *Also note that all of these services will need some path updates to reflect the location of your clone pia repo*
<a/>
*nginx_port.target*
``` bash
[Unit]
Description=nginx pia port target
Requires=multi-user.target
After=multi-user.target
AllowIsolate=yes

[Install]
WantedBy=multi-user.target
```

<a/>
Service for starting and stopping the vpn creation and portforwarding aspect.
<a/>
*pia_portforward.service*
``` bash
[Unit]
Description=starts up script to start the pia plex forwarding process.

[Service]
Type=simple
User=root
ExecStart=/home/theatre/.scripts/manual-connections/connect_vpn.sh
ExecStop=/home/theatre/.scripts/manual-connections/connect_vpn.sh -k
PartOf=nginx_port.target

[Install]
WantedBy=nginx_port.target
```
<a/>
Service for nginx port updating.
<a/>
*port_update_nginx.service*
``` bash
[Unit]
Description=updates the nginx forwarding port

[Service]
Type=oneshot
User=root
ExecStartPre=/bin/sleep 30
ExecStart=/home/theatre/.scripts/manual-connections/nginx_update.sh
PartOf=nginx_port.target

[Install]
WantedBy=nginx_port.target
```
<a/>
After you have created all of these scripts and placed them in the appropriate location (probably in /etc/systemd/system), you can enable them and start and stop both services with the nginx_port.target.
``` bash
# systemctl enable nginx_port.target
# systemctl enable pia_portforward.service
# systemctl enable port_update_nginx.service
# systemctl start nginx_port.target
``` 
<a/>
Now you should have a basic setup using the PIA's manual vpn connection with port forwarding. This general guide can be ported and used for various other setups.

# Resources
 - [Systemd basic guide](/linux/2020-12-30-custom-linux-services)
 - [Man Article on Systemd and .Services](https://man7.org/linux/man-pages/man5/systemd.service.5.html)
 - [Official PIA github repo](https://github.com/pia-foss/manual-connections)
