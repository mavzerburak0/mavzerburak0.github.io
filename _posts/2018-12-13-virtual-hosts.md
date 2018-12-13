---
layout: post
title: Configuring NTP
categories: [sysadmin]
tags: [ntp, ntpd]
description: NTP configuration using ntpd
published: false
---

# Setting up virtual hosts

Virtual hosting allows us to host multiple domain names on a server with a single IP address.

The webserver I will be using for this exercise runs a Debian 8 operating system.

There are three types of virtual hosts available in apache2. These are:
1. Port based virtual hosts
2. Name based virtual hosts
3. IP based virtual hosts

Once you set up one, the difference in setting up the others is fairly minimal.

First, update and upgrade your packages and install apache2 with the following commands:

sudo apt update && sudo apt upgrade
sudo apt install apache2

Test your installation with:

wget <Webserver IP address>

Go to:

/etc/apache/sites-available

If you check the files in this directory, you can see that there are currently two files namely:

000-default.conf
default-ssl.conf

## Name-based virtual host configuration

Make a copy of the file named 000-default.conf with the following command:

sudo cp 000-default.conf 001-namedvh.conf

Open the file for editing with your terminal-based text editor of choice (nano, vim etc.):

vim 001-namedvh.conf

In this file, you can see the opening and closing tags for VirtualHost

<VirtualHost *:80>
...
</VirtualHost>

The lines in between are mostly comments on how to do the configuration.


