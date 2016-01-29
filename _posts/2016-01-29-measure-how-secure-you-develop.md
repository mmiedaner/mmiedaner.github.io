---
layout: post
title: "Measure how secure you develop"
date: "2016-01-29 08:10:38 +0100"
category: blog
link:
filename:
thumbnail:
---


A secure development life cycle has been a well known term for 
quite a while. Despite the fact that not every software company 
has deployed such an approach there is no the 'secure development 
life cycle'. Many variations exist ranging from
[Microsofts example](http://www.microsoft.com/en-us/download/details.aspx?id=29884)
to nearly none as you may encounter out sourcing web page design 
to a tiny web shop. This raises the question: "How can I measure 
the real security gain of my implementation of an SDLC?”

OWASP provides you with the  [OpenSAM] (http://www.opensamm.org/)
- a free framework to determine the maturity of your way to create 
software. They offer a [Cheat-Sheet](https://www.owasp.org/index.php/Secure_SDLC_Cheat_Sheet) on how to set up a SDLC as well. My only remark on 
their approach is that I would like to add two more steps: 

######Step 7 - “Measure" 

and 

######Step 8 - “Improve” 

Clearly this is my personal opinion - take it as such. 


But within this post I do not want to discuss all the possibilities of 
how to set up an SDLC. I would like to concentrate on the two steps 
suggested above: “Measure" and  “Improve”. Metrics especially
during the development are interesting as they let you literally watch 
how your software get more secure or stays secure.


Static code analysis provides you with a lot of insight into how code 
gets created and matures over time. Within the next sections I will 
discuss a few metrics that turned out to be useful for my place of work:


###Maturity metrics:

* An interesting metric is the ratio of the Scrum velocity (a measure of  
the tackled complexity) to the amount of findings per sprint.

* Depending on the length of a sprint you may also analyze the number
of findings opened to the number of findings closed during a sprint.


* As far as it may be traceable you should determine the ratio of 
security requirements implemented per sprint to the amount of total 
requirements and contrast this with  total amount and the amount
of remaining security requirements.


###Code creation metrics:

* The amount of security defects per application is an interesting metric 
- especially once you group your application based on the risk the pose 
to your company or their exposure. Easily you can create a heat map based 
on this data and start to coordinate a campaign to fix the bugs identified.


* Based on tools like [find sec bugs](http://find-sec-bugs.github.io/) you 
can determine how many of your applications are vulnerable to what attack 
or group of attacks.

* To take this even one step further you may as well group your 
applications by risk, department, location, interconnectedness or similar 
factors. 

* An additional metric is to look at the estimated effort for fixing the 
findings. Especially if you think about planning your next sprint it is 
essential to know how much capacity you have for new features.


Besides if you are lucky and your developers are using sonarqube. You do 
have the possibility to tag various rules from static code analysis 
frameworks like [find bugs](http://findbugs.sourceforge.net/) or
[PMD](https://pmd.github.io/) as well as 
[find sec bugs](http://find-sec-bugs.github.io/). Approaches for
tagging vary widely. In larger companies you normally will face some 
security standards or rules that have to be followed by the development 
team. So tag your rules based on that. Such a tag set allows you to 
measure your level of compliance including the increase you make with time.


Although it might help to tag the rules based on international standards 
like the OWASP TOP 10 Active Controls, CWE, SANS and so on.
Here you’ll find a simple [python script](https://github.com/mmiedaner/security/blob/master/metric/SonarMetricsExtractor.py)
that helps you extracting the required data from your sonarqube 
installation.


In a future step this should be combined with dynamic code analysis and 
penetration tests according to these standards as well as test being 
completely of limit. But this will be a completely different blog post?

Cheers!
