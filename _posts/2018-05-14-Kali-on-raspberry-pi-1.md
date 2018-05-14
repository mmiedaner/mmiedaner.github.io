---
layout: post
title: "Kali on Raspberr PI - Part 1"
date: "2018-05-14 08:41:50 +0200"
category: blog
link:
filename:
thumbnail:
---

Kali Linux has been my go-to linux distribution for penetration testing. Normally I do use it as a virtual machine on my laptop.
However there are a few situation where you need such a distro on something smaller. Here's where Raspberry PI comes in handy.
Within this blog post series I will document my adventures playing with Kali on such a small computer.


# Prerequesites #
What do you need to build your own KALI-PI? Basically an Raspberry PI 3, a fast 16GB SD-Card and a laptop/computer of your choice.
Some network equipment like router, cables etc. are usefull as well. Before I started I connected all computers to the router
and ensured that the internet connection is working.


# First Task: Installation #
To install KALI you need to download the current image first. Once it has been copied on the SD-Card you can boot your PI from it.
To do this follow these steps:

1. Download the image
You'll find it in the [Kali Download section](https://www.offensive-security.com/kali-linux-arm-images/). Once you have it unzip
it.

2. Copy it on the SD-Card
This can be done multiple ways. I prefer the commandline:

  dd if=<path to your image file> of=<path to your sd mount point> bs=512k

And of you go.

# Second Task: Regenerate the server key #
Since the server key of KALI's PI builds is widely known you need to regenerate it with these commands:

  rm /etc/ssh/ssh_host_*
  dpkg-reconfigure openssh-server
  service ssh restart
  
Now you can add aditional users and disable SSH login for root. And that's it for today

Cheers !


  

