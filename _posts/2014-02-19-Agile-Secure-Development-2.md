---
layout: post
title: A(-gile) Secure Development Life Cycle 2
category: blog
---

The previous post I argued why a 
Secure Development Life Cycle (SDL) is important. 
Besides a few ideas were pointed out how to start 
with the team - the most important asset you have 
in your company.

##Integration of security experts into the development team
"Hang on - we are security experts - we do not 
write code." Honestly, I am curious if this statement 
is good. Surely, a security expert won't be a battle 
proven senior developer. But he knows a lot of how 
code should not be written and how to exploit it. 
First thing that comes to mind on this topic: Let 
these guys do code review. Who doesn't like that?
How about integrating security professionals into 
your development team. They will be slow in the 
beginning, because they have not been coding for 
a long time. But after short integration phase, 
they are up and running.
On the other hand one may integrate such a person 
only for a limited time. Within that period they 
may build one critical component, like an authentication 
provider or an OAuth service. This period of time 
may as well be dedicated to refactoring and clean up. 
Think about a hardening time or sprint if you are 
doing agile development.
Now let's get deeper into the tooling.

##Tooling
Code analysis is an old topic and various tools 
exist to do this job. However, why not integrating 
them into the nightly builds of your product? Why 
stopping at code analysis tools? Scanners like 
OpenVAS, Nessus, ZAP or BURP have APIs exposed that 
allow their integration into continuous integration 
systems with minimal efforts - if any.
However, integrating them into your CI service is 
the first step. What happens to the findings they 
produce? How to handle false positives - findings 
which aren't a real security whole?

Normally you do bug tracking with some tool - 
generate a short script that helps importing the 
results of a nightly security scan into your bug 
tracker. And while your doing it, you may as well 
take care of the false positives and duplicate 
entries. Nothing is more annoying to your developers 
than getting issues for a false positive and 
that over and over again.

Besides the continuous integration you may also 
add static code analysis to your pre- or post 
commit hooks. Pre commit can stress your developers 
hard, because they get the feeling not being able 
to push any code to the repository. On the other 
hand you ensure, that only checked code is stored 
within the repository. IDEs like IntelliJ IDEA offer 
you such analysis steps as pre commit function - so 
you do not even have to touch your repository for that.

Post commit hooks are executed once the code is 
pushed to the repository. Thereby the analysis will 
be performed on the repository server it self and not 
on the developers computer. So you may pimp your 
repository server in advance to keep your developers happy.

##And after that?
Yep, secure development is not only about tooling 
and education. Periodic penetration tests can not be 
avoided. The amount of findings from these tests 
however can be greatly reduced to your favor by 
ensuring that security related bugs do not enter 
your testing or production environment.

##Release management and hot patching?
These two topics are often neglected when we talk 
about a Secure Development Life Cycle. However, 
just building the software as secure as possible 
is only half of the story. Once your product 
enters the production environment you'll have to 
think about release management and maybe hot 
patching. Hardening releases are not off topic 
anymore. But how often can you release? 
Especially if you are not in an agile environment. 
You really have to think about it.

Read more on the next post . . .
