---
layout: post
title: Security Metrics
category: blog
---

How do you measure security? What are indicators which 
tell you that how secure you really are?


These two questions bother nearly every security 
professional. Especially when he needs to talk to 
higher management to explain the situation and his 
decisions. Of course not all metrics are good and useful.


For example take the amount of attacks recognized 
and blocked by your IPS/IDS. What does this really 
tell you? On the hand you see the amount of possible 
attacks hitting your face to the internet. One may 
estimate the real amount of attacks launched taking 
into account that the IPS/IDS only realizes a certain 
range. This means it misses a certain fraction.


On the other hand successful penetrations of your 
network will not show up within this measurement. 
In case you combine the amount of attacks towards 
your network with other data:

* the amount of unusual connection attempts out of your company
* the amount of data ex filtrated per computer of your company
* unknown ip addresses data was transferred to or that were contacted otherwise
* unknown ip addresses that connected frequently to your network

In a nutshell I suggest you combine the logs from your 
internal IPS/IDS and your IPS/IDS up-front installation.


Patch management is an other good indicator for 
the security of your companies IT. Once you know 
how many patches were tested and rolled out as well 
as how long it took you to do this provides a solid 
argument. But patch management alone is only tells 
you part of the story. Combine patch management with 
incident response metrics. In case of a breach: 
How time do you need to detect the intrusion, 
stop it and patch the system? Besides, combine 
the patch management data your IPS/IDS data 
to see how many known attacks were stopped 
by patching your systems.


Contrary to all technical focused metrics you need 
to take into account that you have employees as well. 
The best it security does not protect you against an 
employee handing over data - for whatever reason.


Awareness is hard to measure, however I do suggest 
that you gamemify this approach. For example: 
Social Engineering / Phishing. Set up a mailing list 
that employees can send suspicious mails to. 
Fill this list with life - do not underestimate 
the amount of time you will spend on answering 
mails. Answer them fast on a very high professional 
level. It takes your employees quite some courage 
to send mails to that list and to admit that they 
feel unsure about the mail send. In addition, 
to make it more fun, send out self-written 
phishing mails to your employees as well and 
reward the first person that returns it to you. 
You may give away a Starbucks voucher to the 
first employee that returns your phishing mail.


On a longer scale, the "decay" of password strength 
is very indicative. After an awareness training for 
a certain department measure the strength of the 
passwords of the employees. Do this on a regular 
basis and plot the results against time. Similar 
things can be performed for various types of awareness 
trainings. Their combination not only yields 
information about the success of the training 
it self. It also helps you to fine tune the 
frequency in which employees should take such lessons.

If you want to continue on this topic - read the book 
by Andrew Jarquith ["Security Metrics"](http://www.amazon.de/Security-Metrics-Replacing-Uncertainty-Doubt/dp/0321349989/ref=sr_1_1?ie=UTF8&qid=1400156889&sr=8-1&keywords=security+metrics).

Cheers!
