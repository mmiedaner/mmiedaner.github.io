---
layout: post
title: "Introduction To Docker Security"
date: "2017-01-16 19:53:48 +0100"
category: blog
link:
filename:
thumbnail:
---

Containerizing your applications has many advantages. Not only can you
achieve a higher degree of separation you also simplify updates, upgrades
and the gain a lot of stability for your environment. On the other hand
using containers comes with its own challenges. Here are just a few 
thoughts.


Solutions like docker rely on the kernel of the host system. In the simplest
case you have a Linux environment running a Linux based container on top of
it. This works based on sharing the kernel and its modules. So, once you
have an exploitable bug within the kernel this bug can be abused either 
via the host system or any of your containers. Not a good situation to be 
in. You have two choices now: Either you virtualise your host system -- 
remember abstraction to the rescue for any problem :) or you make your 
patch management lightning fast and set up various additional security 
measures.  Either way you need to lift some weight. Of course their are 
ways to reduce your attack surface by taking additional measures like 
name spacing, eliminating the use of "root" as much as possible and so on.  


Docker Hub or any other registry for containers is a very convenient and
fast way to build and run your applications. However, it raises the question
to what extend can you keep up with your patch management procedures and
agreements? In addition, how do you ensure that the downloaded containers
only do what they are supposed to? Clearly, I am assuming that every one
is bad person and only focussing on stealing your money - no seriously, 
you should take into account, that you may download a compromised container
that could ruin your infrastructure and your business. How do you protect
against this thread?


On the other hand such a registry would be hosted - in the worst case - 
world readable somewhere on the internet. Taking this into account, it
is dangerous to expose credentials to database servers or any other tier
of your architecture through a container. My personal opinion - stay 
away from committing your containers to any registry outside your own
company. Clearly this will cause some other problems. But it avoids the
simplest way of getting compromised.


But returning to the shared resources as mentioned in the first paragraph.
This fact bears way more implications. Besides exploiting bugs within the
shared resources, if not configured properly, containers could access
resources like directories, file shares, network traffic and so they are
able to extract data or fill up space that should not be accessed. Besides
the data leakage problem you may as well face the distribution of malware.
And finally there is still a chance to simply occupy all resources and
cause a denial of service. Yeah, life can be fun. . .


As in the case of virtual machines you finally faces guest to host escapes.
With containerization this is still a problem. On the one hand due to the
shared resources on the other hand possible due to name spacing and mapping
user like root inside the container to root on the host. This would result
in a direct compromise once a root user could exploit for example a kernel
bug and escape the container. She would be root on the host directly. In
many other situation the escape should be followed by a privilege escalation
to gain full root access. 


One final thought: Solutions like docker run with highest privileges on the
host. Once you enable any remote accessible API on them take into account
that this API may be called from outside your network as well as patch 
management for the container solution to ensure that you do not expose
bug that could lead to a take over of your host systems. The way from the
host to the container is unprotected - at least a file system level. There
are no secrets within the container :) This is one the one hand the beauty 
but on the other hand the devil you are facing using this technology.


In conclusion you increase your security posture significantly by using
containerization products like docker. Keep in mind what the pros and 
cons of it are and use them wisely. Ensure that you drop any unused 
privileges and test all software as severely as in the days without 
containerization. Finally isolation containers via an additional virtual
machine may help to reduce possible damage to a minimum. So, take some
extra care using this approach to improve your application security! 

Cheers!
