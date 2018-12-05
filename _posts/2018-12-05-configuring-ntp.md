---
layout: post
title: Configuring NTP
categories: [sysadmin]
tags: [ntp, ntpd]
description: NTP configuration using ntpd
---

NTP configuration using ntpd
======

The topology I will be using for this exercise is as follows:

```
172.16.88.0/24 srv subnet

172.16.88.100 (S1) will have NTP server installed and broadcast NTP
172.16.88.200 (S2) will take its NTP from 172.16.88.100
```

_All machines in this exercise are using Debian 8 as their operating system._** 

I will first start by installing the ntp package on S1 with the following command.

```
sudo apt -y install ntp
```

Once that is done, you can start making the necessary configurations in /etc/ntp.conf.

Edit /etc/ntp.conf with any editor you like (vim, nano etc.)

This configuration is subject to change depending upon where you are based. Find the suitable NTP servers based on your location and add them after the line that reads:

```
# You do need to talk to an NTP server or two (or three).
```

In my case, I have added these two servers:

```
server clock1.infonet.ee
server clock2.infonet.ee
```

You can also use pools of NTP servers based on your region. As far as I know, ntpd handles them both in the same way except when you use pools, you will get a different NTP everytime a request is made. For the sake of learning, I have also added pools according to my region and commented out the existing default ones by putting a hash sign (#) before them.

```
server 3.ee.pool.ntp.org
server 0.europe.pool.ntp.org
server 2.europe.pool.ntp.org
```

I have added the network range I am using to allow receiving requests.

```
restrict 172.16.88.0 mask 255.255.255.0 notrap nomodify
```

The last two parameters here are access restrictions that you can apply to the subnet.

_The notrap option prevents ntpdc control message protocol traps_. 
_The nomodify options prevents any changes to the configuration_.

To get more information about access restrictions: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/s1-Configure_NTP

I have also added a NTP broadcast for the subnet which will be useful in the second part where I will set up a client that listens to this server for NTP.

```
broadcast 172.16.88.0
```

Now, you can start the NTP service and check if it's running correctly.

```
service ntp start
service ntp status
```

You can also check which NTP server is being used and some other detailed info by running:

```
ntpq -p
```

Output should state the NTP servers that we have specified in the /etc/ntp.conf file. In this case,

```
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
clock2.infonet. .PPS0.	          1 u    3   64  1      2.453  -36.083   0.000
clock2.infonet. .PPS0.	          1 u    2   64  1      3.983  -38.042   0.000
siim.ut.ee      193.40.133.142	  2 u    1   64  1      5.260  -38.220   0.000

_[output omitted]_
```

As you can see, the NTP server that has the least delay is being used first, the others are fallback. Also, third server on the output is coming from the pool we have added (there are two more in the output coming from the pools). 

Setting up a client
------

For the client that will listen on local broadcasts, install ntp as stated above.
 
It is pretty straightforward to listen to local NTP broadcasts.

Edit /etc/ntp.conf configuration file with your preferred text editor.

Uncomment the lines at the end after:

"# If you want to listen to time broadcasts on your local subnet, de-comment the
# next lines. Please do this only if you trust everybody on the network!"

The lines that should be uncommented are:

```
disable auth
broadcastclient
```

Restart the ntp service to make sure the changes take effect and check its status.

```
service ntp restart
service ntp status
```

Check your NTP server and other detailed information by running:

```
ntpq -p
```

Output should state your server's domain name. In my case:

```
     remote         refid   st t when poll reach   delay   offset  jitter
==============================================================================
s1.i803.zz    212.7.1.132    2 u   47   64    37   0.344   121.299 18.472
```

As you can see, my server's domain name is shown in the output. refid here shows the IP address of the NTP server that the first machine is using. Two machines are using the same NTP server which means their times should be in sync.


