---
layout: post
title: The Hacking Process
categories: [ethical hacking]
tags: [CEH, ethical hacker]
description: A brief description of each step involved in hacking
---

## The Hacking Process

To beat hackers, we must know the way they think and act. Gaining access to a system is not an easy task and requires expert knowledge on things such as footprinting, scanning, exploiting a vulnerability in a system. In this blog post, I would like to go through the six steps of hacking into a network or a computer system which include:

* Footprinting and reconnaisance
* Scanning and enumeration
* Gaining access
* Privilege escalation
* Maintaining access
* Removing evidence


### Footprinting and reconnaisance

Although it sounds exciting to dive into hacking your way through a system to gain, say, root privileges, it is not possible to do so without any knowledge of the network you are trying to gain access to. Footprinting and reconnaisance activities include locating, gathering, identifying and recording all the information you could get about the target via various ways including:

* Dumpster diving
	Lots of important information is being thrown away everyday. Dumpster diving is simply going through the trash of a target organization  looking for anything that could be of any value.
	
* Social engineering
	If a hacker believes in his/her social skills, this technique can be quite useful in extracting information from people working at the target organization. In this technique, either on phone or in person or online, a hacker tries to sweet-talk employees into giving out information that comes in handy when executing an attack.

* Internet
	Internet is a hacker's best friend in finding out more about their target. Think of any company website, it includes at least the list of employees, maybe even their e-mail addresses or where they are located.

### Scanning and enumeration

Scanning is generally the active phase of gaining information about the network after the passive step of footprinting and reconnaisance. It includes connecting to a network to get a response. One of the most useful tools for this task is *nmap*. Nmap lets you send a request to a server and see various information about it, such as open ports and applications running on those ports which can come in handy. Although usage of nmap is easy and fast, companies now use intrusion detection systems which detect and warn the IT Security teams of possible scans. The workaround of this is to set the scan to be very slow in order not to trigger the IDS. Also, if an attacker disregards stealth, he/she can even use vulnerability scanners which are fast at detecting vulnerabilities on a server. However, these tend to be very noisy and easily detectable.

### Gaining access

After vulnerabilities are found and the hacker has the right tools, the real action begins. Gaining access to a system is possibly the most satisfactory step of the hacking process. As mentioned above, access can be gained in many ways. For example, a hacker might find an old version of an application on a web server and using a vulnerability found via Internet (e.g. on *https://www.exploit-db.com/*), he/she can infiltrate a system.  

### Privilege escalation

Although gaining acccess is satisfactory, executing whatever command you'd like on a system can certainly be its competitor in this regard. If gaining access is entering from the doors of a highly-protected kingdom, gaining root access (or administrator rights) is becoming the king in that kingdom. There are many ways of escalating the privilege depending on the operating system and the version of that operating system. These will be discussed further in another blog post. 

### Maintaining access

Now that the hacker gained access and escalated his/her privileges to do anything an admin can do, it is time to try ways to maintain their access to a system to get in and out as they please. _Rootkits_ are essential tools for this purpose. A rootkit is a collection of tools, rather like a tunnel to a system that only the hacker knows about. They generally hide their presence and hackers' malicious activities on a system. 

### Removing evidence

This step goes hand in hand with maintaining access. No criminal would like to leave any evidence behind and hackers are just the same. They plant rootkits and backdoors to hide their activities and cover their tracks. Tracking down and/or erasing log files, hiding affected files and even patching up the vulnerability they used to access the system, so that other hackers cannot access the same system are other ways used by hackers to keep themselves safe and anonymous.


Detailed blog posts for each step and tools used in them will be written in the future.

References:

* [CEH - Certified Ethical Hacker Version 10 Third Edition - Michael Gregg, Omar Santos](https://www.amazon.com/Certified-Ethical-Hacker-Version-Certification/dp/0789760525/ref=sr_1_1?crid=339ZU06MPHMPR&keywords=certified+ethical+hacker+ceh+version+10+cert+guide&qid=1561720964&s=books&sprefix=ertified+Ethical+Hacker+%28CEH%29+Version%2Cstripbooks-intl-ship%2C264&sr=1-1)