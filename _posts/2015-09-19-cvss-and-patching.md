---
layout: post
title: "CVSS and Patching"
date: "2015-09-19 17:18:48 +0200"
category: blog 
---

CVSS as vulnerability rating score has been around for some time now. 
Currently it is in version 2 and version 3 is reaching the final reviews. 
Therefore I will focus on version 3. [CVSS](https://www.first.org/cvss)
 provides you with three different scores for one vulnerability. 


The BASE score. It rates just the vulnerability based on
various factors like complexity of the attack vector, requirement of 
privileges, user interaction and so on. It also considers the impact 
on confidentiality, integrity and availability of the
vulnerable system. 


The TEMP-Score takes into account the maturity of an existing exploit code,
if patches by the vendor or workaround recommendations are provided. So 
the TEMP-Score considers time and human actions as an additional factor.


The ENVIRONMENTAL-Score is the last CVSS score and takes into
account various conditions under which you run your systems. So one 
vulnerability may impact workstations more than servers in your data center.
This is taken care of with this scale. Mathematically one could derive all
other scores from this one - but I don't want to get into this.

What does a vulnerability rating help you with your patch management? This
question is debated strongly. On the one hand, relying on a standard to
prioritize your patches and their roll out frequency is a good argument for
management, compliance or controlling questions and so on. Also all you 
are doing is critical things first. True - there hardly anything wrong 
with that.
However, rolling out patches based only on their CVSS-Score creates a lot of
work. Most vendors provide you with the BASE-Score only. So you calculate
your environmental score based on that. Running a large data center with a
very heterogeneous soft- and hardware landscape - have fun :)

Besides [Allodi and Massacci](https://media.blackhat.com/us-13/US-13-Allodi-HOW-CVSS-is-DOSsing-Your-Patching-Policy-WP.pdf) compared the CVSS ranking 
against the availability of exploits in metasploit and the black markets. 
Their conclusion:

You should patch when:

a) their exists an exploit on the black market (mainly medium-high CVSS ranked vulnerabilities)

b) a proof of concept exploit exists for the vulnerability and it does not
require authentication and can be exploited over the network (mainly
medium-high CVSS ranked vulnerabilities)


But still not every system has the same accessibility - a point Allodi and Massacci discuss as well. They recommend patching the internet / external 
network facing systems asap and systems in highly secured networks later on.
In my opinion this is a good advice. 
I would like to add one adjustment to that: Besides this 
prioritization an overall very good standard of patching will keep you save.
No matter how restricted the access to the system is ensure that it gets 
patched and updated within a reasonable interval, like 90 - 120 days.

This approach should be measured - doing a good thing and talking about it!
Report how many systems violate this interval and compared to their 
criticality. In case you have a well tuned security incident and event 
monitoring system (SIEM) in place - correlate the amount of offenses 
created by network segment or system against the violation of the patch 
interval. 


Cheers!
