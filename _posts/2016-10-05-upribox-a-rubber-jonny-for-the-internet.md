---
layout: post
title: "UpriBox - A Rubber Jonny For The Internet"
date: "2016-10-05 16:26:11 +0200"
category: blog
link:
filename:
thumbnail:
---
As we packed our things for a beach holiday, I was looking for something
to shield my laptop and smart phone from the wireless access we booked
together with our cottage at the sea. It should be small, fast and secure -
basically a rubber johnny for the internet. 

But how to build it and on which platform? 


While cruising through the internet I came across 
UpriBox - the usable privacy box. In conclusion it is a distro for your
raspberry pi which offers you a solid filtering solution for accessing the
internet. You can find out more at: [https://upribox.org/](https://upribox.org/). Besides simple filtering and cleaning the incoming web traffic 
UpriBox allows you as well to route all your traffic through TOR.
Clearly both ways do not protect you against a man in the middle by your
provider. In our case, I was considering injected adds and a possible 
hijacked access point to be the most realistic threads. And it turned
out to be that way. The access point was injecting adds. But, thanks to
UpriBox and the filters included, these were successfully blocked.


Now let's skip the holiday story and dive a little bit deeper into UpriBox.
You can download the image for your raspberry pi freely from github: [https://github.com/usableprivacy/upribox](https://github.com/usableprivacy/upribox). To make it work smoothly I had to buy an additional WiFi adaptor. For
my raspberry pi II I choose a TL-WN722N as recommend on the projects github
page. From that point on it was simple plug-n-play. Put it all together,
power it up and change the password (!!). 


UpriBox boots and spins up two different WLANs: "Slient" and "Ninja". 
While both filter adds and other nasty stuff the "Ninja" WLAN also routes 
all traffic through TOR. Meanwhile UpriBox offers a third possibility: 
You can configure a VPN to allow complete encryption of your traffic and
getting maximum privacy while using unknown internet connections. In 
addition, it is very nice to see that UpriBox checks every four hours for 
new filtering rules and DNS. Besides these, you can access the distro via
SSH - take care to change that password as well, when you set up the box.
From this point on you an add your own rules to privoxy and the DNS.


What did I miss? Only one minor point - but I must admit I haven't spent
much time to investigate and fix it. But, it will be covered in a following
blog post. At our cottage I had to connect the
raspberry via cable to the provided internet access. That was a little bit
cumbersome since the WLAN adaptor was not as strong as to flood more than 
2 rooms of the 4 and a half cottage, nor did it reach the veranda. So no
internet while chilling in the evening sun. Besides that - it was fun 
playing around with UpriBox. In comparison with FruityWifi, it was way 
easier to set up and use. Password changes were the "hardest" thing to do ;)


So, you are planing your next trip? Take a look at UpriBox and turn your
raspberry pi into internet rubber johnny (raspberry flavored :) ).

Cheers! 
