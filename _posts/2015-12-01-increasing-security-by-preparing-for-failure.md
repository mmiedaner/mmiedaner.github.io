---
layout: post
title: "Increasing security by preparing for failure"
date: "2015-12-01 18:05:56 +0100"
category: blog 
---


Finical industry has long learned a lesson I miss when we talk 
about IT- and Information security. In IT-Security we spend a 
lot of time and effort to detect a possible breach as well as 
to harden our systems. However not much energy gets invested 
in how to minimise the impact of a possible breach. Of course 
we do segment our networks to slow down any possible intruder. 
We do apply the laws of separation of duty and least privilege 
to reduce possible harm done to our systems and data. Honeypots 
and SIEM solutions get installed to easily catch the elephant 
in the room. Besides all that not much energy get’s spend to 
ensure that the impact of a breach is reduced to a minimum.



Let us take a look at banks and how one could reduce the 
impact of a possible bank robbery. First try to secure your 
staff by bullet proof glas, surveillance cameras, alarm buttons 
and so forth. So far this could be compared to what we do in 
IT-Security. A step forward within the example of the bank is 
to reduce the amount of cash available at a single location. 
Besides a separate bag of well indexed money could be prepared 
for the possible event of a bank robbery. So it would be 
extremely easy to trace the stolen money. Also the maximum 
amount of money lost is reduced to a well calculated and 
traceable amount.



How could we implement this in IT- and Information security?
The first thing that comes to mind - use fully encrypted 
databases. In case of an publicly available SQL-Injection 
vulnerability only encrypted data could be stolen. However to 
process these data you will need to decrypt it within your 
application. So the key to encryption has to be at least 
in memory of the servers respectively. Once an attacker 
would escape the runtime of the application exposed she 
would be able to retrieve the key and steel the unencrypted 
data. By the way an interesting discussion of encrypted 
databases and their usage was given by Peter Wayner
in the chapter "Doing Real Work Without Real Data" in the 
book [Beautiful Security](http://shop.oreilly.com/product/9780596527488.do).



Although besides SQLi the attacker could abuse other flaws 
to obtain the desired data: logical, access control, direct 
object references and so on. On the other hand you place your 
data on several databases. Think about caching - in a company 
the web presence and portals do not request all data at all 
time. They are rather limited to a certain set of data that 
the customer do use most of the time. So, what about 
introducing a caching layer hold the most commonly used data 
in a separate read only database. New data and changes on 
existing data get written to the real database. So all that 
is left is replicating data changes in an appropriate interval 
to the “caching database” for your web applications. However 
since the main database is never read by a web application 
and the queries could be strictly filtered for the main 
database and the caching database as well - this resembles 
the bag of prepared money for a bank robber.



An other question - To what extend could an IDS help? 
Hmm - despite the saying that “IDS is dead” it is an interesting 
idea to filter all outgoing traffic for specific information. 
Once a filter hits the outgoing traffic all packets get dropped 
by an internal firewall or better replaced by traceable information.
However a bank robbery is a slightly simplified situation because 
it is restricted to physical access to the bank. In an IT- or 
Information security breach the thief could be well outside the 
country and hide his trace very well. This makes catching the thief 
way harder than catching someone who is required to have physical access.
However there is the possibility to make certain documents call 
home once they were opened. Sure thing this will not work when 
the clever thief opens the data off-line. Although her firewall 
may alert her and cause further protective measures taken by the thief.



Last but not least to reach data that have a higher impact when 
stolen you need to navigate through an application in general. 
Along that path you could easily integrated various steps of 
authentication. Again a very simple example is in online payment. 
After reaching a certain threshold for a single transaction you 
are asked for a pin to authorise your credit card payment. 
Thereby it is ensured that you not start the transaction from the 
same phone you will receive the authorisation pin to. 
So we combine various steps:
a) you need to enter a pin send to you
b) you need to have a separate channel for receiving the pin - 
separate from the channel you started the transaction on.




Google also takes into account the geolocation your request 
comes from. This is as well an indicator that something might 
be wrong because you simply can not travel physically from 
England to China within five minutes and get online again to 
log into your email. So there must be something suspicious 
about the requests and you get asked for a second level of 
authentication like solving a captcha. Those may not be the 
only thing. So separating parts of your application by 
requesting an additional authentication helps. But the 
usability of your applications suffers from it. So you might 
start with soft authentication methods like analysing the speed 
and rhythmic pattern your users type. And once this differs 
significantly start asking for additional authentication - 
not only renting your password.



But not only web applications are the only way to breach your 
company. Employees and their workstations are targets as well. 
The first thing that comes to mind is application white listing 
and anti-virus software. Let us skip anti-virus for the moment 
and focus on application white listing. Sure thing, the more 
you control the software that is available on a workstation 
the better you are able to control its attack surface. On the 
other hand profiling the work-habits of your employees to some 
extend could help you define anomaly rules for your host 
intrusion detection system (HIDS). However this violates the 
privacy of your employees - at least in Europe :)



So far - but do not forget to make sure that you know and 
constantly practice how to communicate a possible breach 
as well as how to clean it up.



Cheers!
