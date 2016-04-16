---
layout: post
title: "Battle Of Machines"
date: "2016-04-16 15:49:14 +0200"
category: blog 
link:
filename:
thumbnail:
---
The battle of Machines or how to bring automated pentesting into your
development life cycle - this is what I will talk about today. But what
drives someone to such an idea? There are a few factors. On the one
hand agile development and maintenance techniques have been established
in most companies. This clearly forces the security teams to hurry up
and finally to reorganize their way of doing things. Why? Because
deployments into the production environment will occur after every sprint.
This could be as often as every other week. So, how to ensure that no
additional vulnerabilities have been introduced?

Besides this speed up in the development team the demands on applications
have increased. This is partly due to many libraries and tools provided
as open source that can be easily integrated in existing applications to
add new features. So you have an source of possible vulnerabilities that
could be completely out of your control, when such libraries are loaded
at run time from a third party. However, the demand for integrability
and interaction with other services has dramatically increased. Just take
the ubiquitous Facebook login button as an example. Customers expect 
simplicity and easy to use software, which partially drives your development
team to such decisions.

What to do? Automate part of your pentesting tools and hand them over
to the development team. This gives them the chance to find vulnerabilities
fast and fix them when they have at least some time. The best way to do
this is to start with the integration server like Jenkins or Bamboo. 
Both allow you to start a script as part of the build process. So why 
not scripting tools like OWASP's ZAP, Burpsuite, Metasploit and so on 
to scan your application after each build and deployment into a test 
environment? 

The technical steps like creating the scripts will be discussed in the
following posts. They are one key to the kingdom. But way more important
is the process that you design around the build jobs to ensure that the
results of the scans do not get lost and the vast amount of reports does
not kill your productivity. You should consider of the following questions:

* Who is responsible for triggering the scans? 

* Who is responsible for coordinating how to fix the findings from the reports?

* How often should the scans run?


From the experiences I collected over the last five years establishing
such practices within agile development teams I found that:

* Scans should be triggered on a periodical basis, e.g. every Sunday night.

* A lead developer or Scrum Master should coordinate the work on the findings.

While the later part could be automated by adding an other script or tool
like [ThreadFix](http://www.threadfix.org/) from Denim Group the key
to success is that all findings get transported into a ticket system asap 
and that one person, like a lead developer, scrum master or product owner 
has an eye on them. Unfortunately tickets get lost over time if they get
not prioritized high enough. But too many high priority tickets loose their
value fast easily. So clear rules need to be established on how to 
prioritize certain vulnerabilities. These rules may not be the same for 
every application, but should enforce that a build terminates as 
unsuccessful once certain vulnerabilities are found and no deployment 
of that code should take place. I will discuss this point in greater detail
in an other post within this series on the "Battle of Machines".


Finally, having established such a cycle is one thing - think about metrics
to present your results not only to the development teams but also to
management. Do good and talk about it!! A few suggestions on useful metrics
can be found [here](/measure-how-secure-you-develop/).


The following posts will guide you on how to integrate tools and scanners - 
so stay tuned!

Cheers.
