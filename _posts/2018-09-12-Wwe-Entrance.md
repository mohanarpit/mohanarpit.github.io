---
layout: post
title: WWE Entrance Music
published: true
tags: #fun, #golang, #wifi
---

Everyone deserves an entrance music to announce their arrival into a room. I think this was the biggest perk
given to WWE wrestlers. In an attempt to replicate this behaviour, I wrote a fun little program in Golang that you 
can view [here](https://github.com/mohanarpit/wwe-entrance). 

### Basic Design

A user's phone will invariably connect to your home/office Wifi network before they reach the door. I've tried to leverage
this fact in building the application. The workflow goes as follows: 
* Continuously poll the Wifi network to check for any new devices that have connected recently. 
* If a new device is found, compare it's mac address to a pre-configured list of devices.
* If a match is found, play a pre-configured sound file on the speakers.

This program can be run on a Raspberry Pi or a discarded laptop in your possession. It just needs to be online and 
connected to the Wifi and speakers at all times.

### Challenges

One of the biggest hurdles I faced was to reliably get a list of devices connected on a local network. 
While there are many tools such as `nmap` and `arp-scan`, they weren't proving to be reliable. For example, `nmap` (by default) relies on PING scans to locate devices. Most devices on the other hand don't respond to ICMP requests reliably.
Infact, most devices deem such network scanning behaviour as malicious and the defaults are set to protect the user from 
such behaviour. iOS was notorioiusly hard to detect reliably. There are work-arounds, but I was hoping to not complicate
the code too much. At one frustrating juncture, I even considered scraping the router admin interface to get a list of connected clients.

I have a DLink DIR-800 router which doesn't support DD-WRT firmware. I hear that DD-WRT has the 
capability to publish this information over some queue, but unfortunately, this wasn't an option for me.

### Solution

I thought, if the `arp-scan` from my machine wasn't reliable, would it be any different if I performed it on the 
router itself? Luckily, my router does support Telnet connections. I logged into my router via telnet and surprisingly it opened a full fledged shell! That's incredible. 

```bash
$ telnet 192.168.0.1 23
Trying 192.168.0.1...
Connected to ralink.dlink.com.
Escape character is '^]'.

ralink login: admin
Password: 


BusyBox v1.12.1 (2014-12-11 15:09:57 CST) built-in shell (ash)
Enter 'help' for a list of built-in commands.

# echo $SHELL
/bin/sh

```

Great, so now all I needed to do was perform an `arp-scan` from the router and parse the results. 

On Linux systems, `arp-scan` reads the values from the file `/proc/net/arp`. So, instead of using a command,
I simply read that file and parsed it's contents. 

```bash
# cat /proc/net/arp 
IP address       HW type     Flags       HW address            Mask     Device
192.168.0.103    0x1         0x2         11:11:11:11:11:11     *        br0
192.168.0.102    0x1         0x2         22:22:22:22:22:22     *        br0
192.168.0.104    0x1         0x0         44:44:44:44:44:44     *        br0
```

A **0x2** flag indicates that the device is connected, while **0x0** indicates that it's not. 

**N.B**: It does take a little bit of time for the ARP file to reflect any disconnections. The ARP cache on some devices
 may even be 4 hours. Your mileage may vary. But new connections were fairly quick to be reflected here.

### End Result
I tied it all together in a tiny, fun utility (source code available [here](https://github.com/mohanarpit/wwe-entrance)).
I had an old Sony Vaio laptop lying around which I dusted and brought out of retirement to run this code.
Now whenever I enter the room/office, I'm preceded by my favourite song! 

*Handy Side-Effect*: After configuring a few friends phones, I know who's visiting me before they even ring the door bell.

### Other Applications

Your could also use this utility to add some personalization for colleagues in your office. Can be a nerdy differentiator 
for smaller companies and startups.

### Future Work
Since, I only have 1 router at home, I can't test this program with other models and manufacturers. If you do find this
project interesting, I'd love to hear how you can connect to your Wifi router via CLI. I'll make enhancements to the 
project accordingly.