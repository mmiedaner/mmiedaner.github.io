---
layout: post
title: A (-gile) Secure Development Life Cycle 1
category: blog
---

What is a Secure Development Life Cycle?
What are we talking here about? Basically 
it's changing the way you develop your product 
into a way to avoid security wholes in every step: 
From the conceptional to the design phase and 
finally into the development / engineering phase 
and (mostly ignored) the release management. 
This said, we are focussing on a different way of 
thinking. Security considerations are not part of 
the QA anymore. It is important how you design, 
build and manage your product.
Especially in the agile world security seems to 
be left to the QA and mostly postponed until some 
unknown day after the official "go live". 


#Why should I care?
Considering security implications already while 
defining the requirements saves you time during 
the development and testing phase - no matter if 
you working in an agile or classical environment. 
You thought of it in the beginning and do not have 
to "fix something" that could have been solved early on.
So you are saving money - no extra time to spend on fixes.
Looking at the big players like Adobe, Microsoft, 
Oracle - you save your face. Especially when you 
are a smaller company than these big guys you need 
your face and reputation! You can help to keep it 
up by switching - as the big players did - to a 
secure development life cycle. So breaches, public 
defacements and really bad news like that can be 
reduced to a low level. Clearly speaking you can't 
eliminate security holes in your product - but you 
can make it as hard as you can for any attacker. 
This as well, saves you money. Money that Adobe, 
Microsoft and Oracle are currently spending to 
rebuild their reputation and money they lost due 
to bad press.


#What can I do?


##Requirements and Threat Modeling
Different methods exist to estimate the risk a 
certain feature or requirement will add to the 
overall exposure of your product. Of course we 
can not think about every possible attack for 
obvious reasons. However continuous threat modeling 
with the whole team helps to keep your people aware 
of the possible risks and helps them during the 
implementation and testing phase.

Also you - as a product manager / product owner have 
a metric to measure the exposure. This will not only 
help you when talking to the security guys.


##The Development Team
There are many ways to the improve security within 
an development life cycle. However not every one 
yields the appropriate results. Making your developers 
get an respected certification is definitely one way. 
But how long does that last? In my opinion you're down 
to a view month than the old habits will dominate the 
development process again.

Programming techniques tend to last for a longer time 
than certifications. However, in this case there is 
way more work involved. Extreme Programming like 
Pair-Programming definitely helps. Not only do the 
programmers perform a code review as they type. They 
also are forced to question their decisions constantly 
and justify them in front of each other. Although one 
programmer may forget or slip a classical pattern the 
other programmer has a good chance to catch this 
potential problem right when it's being created.

Besides Pair-Programming Test Driven Development is 
a good choice. Encouraging a programmer to include 
security related test in his regular testing efforts 
is a challenge - given that the knowledge about attacks 
has to be transferred. However, at this point the 
security people could be of great help and basically 
prepare test cases for the developer.

One important step to simplify the development of 
secure software is to build a catalog of patterns 
and libraries which are approved to be secure. Clearly 
putting this catalog together once doesn't help you 
much. You need to work on it constantly. Programmers 
do prefer the "newest" versions of their libraries 
at hand. By the way - one you start setting up the 
list of approved libraries and patterns make it a 
repository immediately. Thereby you will ease up 
work for both - its maintainer and the user.

The next post will continue this topic :)  Stay tuned.
