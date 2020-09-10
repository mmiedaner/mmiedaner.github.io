---
layout: post
title: "Kali Is Your Host"
date: "2016-03-29 20:35:33 +0200"
category: blog 
link:
filename:
thumbnail:
---
Rules to follow: 
1. Do I have a good head line?
2. Do I have a good hook line?
3. Can I add more value to my customers / readers?
4. Do I have a good conclusion / call to action?
5. Does the post look good?
6. Three values / take home messages - which are they?

This blog post is a simple illustration how to set up a guest WLAN 
based on a regular raspberry-pi 2 and the appropriate kali image.
It will show you how to install and configure everything including
a few tips on how to restrict the WLAN access for your guests,
breaking SSL and so on. . . I do expect you to be familiar with
the linux commandline - mainly bash and linux itself.


First of all - get your raspberry-pi 2 and an sd-card that is 
at least 8 GB in size. The Kali Linux Distro for raspberries is
available [here](http://docs.kali.org/kali-on-arm/install-kali-linux-arm-raspberry-pi)
After downloading the image you copy it to the sd-card as follows

	start your main linux box and insert the sd-card

	issue the following command in bash-shell

	dd if=/path/to/your/kali/image of=/path/to/your/sd-card bs=512k

Once everything is copied onto the sd-card unmount it and put it back
into the pi again. Now wire up the pi to a screen or tv and the network.
You will see how Kali boots and if everything works fine, you will the
slim GDM-Login Mask. Your credentials are root / toor - pretty simple, eh?
Once you are logged in you should regenerate the ssh-keys of your Kali server
as folows:

	rm /etc/ssh/ssh_host_*
	dpkg-reconfigure openssh-server
	service ssh restart

Since I do not like to expose root-access to the outside of a server, I will
now add another user as follows:

	useradd -m username
	passwd username
	
	usermod -a -G sudo username
	chsh -s /bin/bash username

The last two lines add the user to the group sudo and make sure that your
login-shell will be bash. For further convinience I do like to install 
aptitude as well via:

	apt-get install aptitude

From here on it is pretty straight forward - after updating the system,
you should install the following packages:

* hostapd 
* isc-dhcp-server

Afterwards you need to tweak their configuration as follows:

Edit the /etc/dhcp/dhcpd.conf by commenting out these lines:

	option domain-name "example.org";
	option domain-name-servers ns1.example.org, ns2.example.org;


You should as well asure that you control the DNS by uncommenting this
line:

	# If this DHCP server is the official DHCP server for the local
	# network, the authoritative directive should be uncommented.
	# authoritative;

And finally pin the DHCP server to your interface of choice: WLAN0
by adding this line to the configuration file:

	INTERFACES="wlan0" 


2. Configure it as a WLAN access point on demand.
Now shutdown your WIFI-Interface via:

	sudo ifdown wlan0

Afterwards edit the  /etc/network/interfaces as follows:

iface wlan0 inet static
  address 192.168.42.1
  netmask 255.255.255.0


To configure the access point you need to create this file:
	
	/etc/hostapd/hostapd.conf

with this content:

	interface=wlan0
	driver=rtl871xdrv
	ssid=Pi_AP
	hw_mode=g
	channel=6
	macaddr_acl=0
	auth_algs=1
	ignore_broadcast_ssid=0
	wpa=2
	wpa_passphrase=Raspberry
	wpa_key_mgmt=WPA-PSK
	wpa_pairwise=TKIP
	rsn_pairwise=CCMP

But make sure that you change the parameters:
interface, driver, ssid and wpa_passphrase - so it will be
your own.

In case you can not find the driver rtl871xdrv within your
installation you need to install the package "firmware-realtek". You
will find it easily by searching for "realtek" from
within aptitude. Make sure that the package you install
has the "firmware" part in its name. It lists as well the
wifi-dongles it supports. 

Afterwards ensure that the hostapd service finds
its config by uncommenting in this file:

	/etc/default/hostapd

the following line:

	DAEMON_CONF="/etc/hostapd/hostapd.conf"





Now Continue with:
Configure Access Point

at
https://learn.adafruit.com/setting-up-a-raspberry-pi-as-a-wifi-access-point/install-software

Grap a list of IPs to ban from here:
http://pgl.yoyo.org/as/

