---
layout: post
title: Setting up virtual hosts in apache2
categories: [apache2]
tags: [virtual host]
description: This is to show the three types of virtual host configuration in apache2
---

# Setting up virtual hosts

Virtual hosting allows us to host multiple domain names on a server with a single IP address.

The webserver I will be using for this exercise runs a Debian 8 operating system.

There are three types of virtual hosts available in apache2. These are:
* Port-based virtual hosts
* Name-based virtual hosts
* IP-based virtual hosts

Once you set up one, the difference in setting up the others is fairly minimal.

First, update and upgrade your packages and install apache2 with the following commands:

```
sudo apt update && sudo apt upgrade
sudo apt install apache2
```

Test your installation with:

```
wget <Webserver IP address>
```

This should download the Apache2 It Works! page. 

Alternatively, you can install curl:

```
sudo apt install curl
```

Then issue:

```
curl <Webserver IP address>
```

This should display the HTML of the It Works! page on your terminal. Go to:

```
/etc/apache/sites-available
```

If you check the files in this directory, you can see that there are currently two files, namely:

```
000-default.conf
default-ssl.conf
```

## Name-based virtual host configuration

Make a copy of the file named 000-default.conf with the following command:

```
sudo cp 000-default.conf 001-namedvh.conf
```

Open the file for editing with your terminal-based text editor of choice (nano, vim etc.):

```
sudo vim 001-namedvh.conf
```

In this file, you can see the opening and closing tags for VirtualHost

```
<VirtualHost *:80>
...
</VirtualHost>
```

The lines in between are mostly comments on how to do the configuration. Change the ServerName to your domain.

```
ServerName <yourdomain>
```

Set DocumentRoot as where you will keep the files related to your website.

```
DocumentRoot /var/www/example
```

You can also rename your log files according to your domain name in order to avoid confusion as to which virtual host the log file is related to in the future where you might have multiple virtual hosts.

Create an index.html file in the directory you have specified for DocumentRoot and write basic HTML specific to this virtual host. For example:

```
<!DOCTYPE html>
<html>
    <head></head>
    <body>
        <h1>(yourdomain) it works!</h1>
    </body>
</html>
```

Then, you can use the command below to enable your site:

```
sudo a2ensite
```

If you have multiple sites and you would only like to enable specific sites, you can use the .conf file created for that specific virtual host to enable it only:

```
sudo a2ensite <filename>.conf
```

This command creates a symbolic link to the site in /etc/apache2/sites-enabled to allow apache server to actually serve the site.

Reload apache2 to allow for new configurations to take effect:

```
sudo service apache2 reload
```

Test your configuration by viewing the HTML content of the site:

```
curl <ServerName>
```

## Port-based virtual host configuration

apache2 listens on port 80 by default, you can make it listen on other ports as well by editing:

```
sudo /etc/apache2/ports.conf
```

When you open this file for editing, you will see this line:

```
Listen 80
```

after the explanatory comments. Add the following under the first Listen:

```
Listen 8000
```

This will allow apache2 to listen on both ports 80 and 8000.

Going back to /etc/apache2/sites-available directory, you should create a new .conf file for your port-based virtual host by copying one of the other two that's available already.

```
sudo cp 001-namedvh.conf 002-portvh.conf
```

Open 002-portvh.conf for editing with a terminal-based text editor of your choice (vim, nano etc.):

```
sudo vim 002-portvh.conf
```

It is very much similar to what is done in name-based virtual host configuration with only difference being the change in VirtualHost opening tag and port addition to ServerName field.

```
<VirtualHost *:8000>
...
    ServerName <yourdomain>:8000 
```

There is nothing more to tweak other than adjusting the previous configuration to your new domain.

Keep in mind that you still need to use a2ensite command and then reload apache2 for the new configuration to take effect.

## IP-based virtual host configuration

You will need to add an IP alias to your webserver for this. Open /etc/network/interfaces with a terminal-based text editor of your choice (vim, nano etc.)

```
sudo vim /etc/network/interfaces
```

Add the following lines (replace ip-address with an IP on your network):

```
auto eth0:0
iface eth0:0 inet static
address <ip-address>
netmask 255.255.255.0
```

This will create an IP alias on the interface you have specified (in above case, eth0).

Restart your networking service to make sure everything still works.

```
sudo service networking restart
ping google.com
```

If the ping command results in packet loss, check your configuration. If everything works as expected, create another file in /etc/apache2/sites-available for your IP-based virtual host.

```
sudo cp 000-default.conf 003-ipbasedvh.conf
```

Open the newly created .conf file for editing:

```
sudo vim 003-ipbasedvh.conf
```

Change the opening VirtualHost tag to:

```
<VirtualHost <ip-address>:80>
```

with ip-address being the IP address that you have used in /etc/network/interfaces file to create an IP alias for your webserver.

There is no other difference to IP-based virtual host configuration from the other two types of configurations. 

Again, don't forget to run a2ensite and reload the apache2 service for the new configuration to take effect.

References:
* [Apache Virtual Host Examples](https://httpd.apache.org/docs/2.4/vhosts/examples.html)
* [maketecheasier - Setting Up Name-Based Virtualhost Apache](https://www.maketecheasier.com/name-based-virtualhost-apache/)

