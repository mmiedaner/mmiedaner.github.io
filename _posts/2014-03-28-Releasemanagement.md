---
layout: post
title: Relasemanagement and Security
category: blog
---

How do you handle security related issues 
as a release manager? What if you're in an 
agile world as a product owner?


What options for releasing software do we have?


##1. Agile
You release minor increments on a frequent basis. 
Based on this you are able to fix security issues 
very quickly assuming that you know of them. But 
what if you don't? How many steps (releases / 
sprints / cycles) will it take you until you fixed 
all of them determines the time window you are 
exposed. However this window does not close once 
the final release is rolled out. Honestly you are 
still in the position that older vulnerabilities 
remain unknown or that the currently developed 
fixes do not close the security wholes completely.
But, given that you analysed all the findings in 
depth and estimated the maximum impact of each 
severely you're in a very good position. Starting 
with prioritised list, working on the highly 
critical issues first you are on a very good 
track! Keep on going!

On the other hand you may face very very 
rapid deployments, like TWITTER or AMAZON do. 
In such a case you must rely on automated 
security testing and strong secure 
development life cycle.

##2. Rolling releases
Rolling releases are established for example by 
various Linux distributions. In such a model every 
package of your Linux distribution follows it's on 
release cycle. At a certain point in time you "freeze" 
all your software packages and call it a major 
release. This is interesting, because you have to 
take security aspects into account for every single 
release of every single component of your software 
portfolio. Also you need to take a closer look at 
it once you are preparing for your major release. 
Compared to the agile world - you are on a slower 
track. This might be helpful - but still there's a 
lot of work. It is also more complex, because you 
have several systems interacting with each other 
and facing their own security problems.

##3. Major and minor releases
Major and minor releases are normally rolled 
out on a very fixed schedule. After releasing 
one version your able to fix vulnerabilities as 
they come along. After a certain time within you 
release cycle - normally around the middle between 
to releases you'll have to close on additional 
features and bug fixes which were included on the 
side to ensure the final quality. From that moment 
on, every vulnerability that's reported will be 
fixed within the next release. The same holds for 
vulnerabilities you have not had the time to fix. 
Within this model your window of exposure is the 
longest. However, assuming that every thing goes 
as planned you also have the most time for testing 
and ensuring the security of your product(s).

