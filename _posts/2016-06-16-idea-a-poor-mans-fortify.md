---
layout: post
title: "IDEA - A poor mans fortify"
date: "2016-06-16 17:24:39 +0200"
category: blog
link:
filename:
thumbnail:
---
Have you ever done code review and regretted that you have no tool
like HPs Fortify? Well, there are alternatives, but at the end of the
day - Fortify is the way to go. Luckily InteliJ produces its IDE called
IDEA. This tools comes in very handy for code review - also it is intended
for developers. There are several plugins like code iris to simplify your
tasks as a code reviewer. Some of them also integrate with common code
repositories and issue trackers. This helps you enormously - but within
this post I would like to give you some advice on how to do a security
focussed code review with IDEA without any additional plugins - a poor mans
fortify.

Besides the tooling you need a rigorous approach to proceed during your
code review. You may either follow the [OWASP Code Review Guide](https://www.owasp.org/index.php/Category:OWASP_Code_Review_Project) 
which I will not cover in great detail or take a closer look at my previous
blog post [reviewing code for fun and profit](https://mmiedaner.github.io/reviewing-code-for-fun-and-profit/) 
which describes a very similar approach and is much short. Which
ever way you go, I highly recommend starting with planing your analysis
step by step. If you have not done any code review to this point and would
like to get more recommendations - talk to me.

OK, but now let's get our hands into some code. Grep any project you are
interested in analysing and if you haven't already installed [IDEA](https://www.jetbrains.com/idea/download/)
now is a good point to do that. For this post I prepared an inspection policy for your IDEA that helps
you automating the points explained below. You can get it 
[here](https://github.com/mmiedaner/security/tree/master/code_review). 
To import it open

```
Analyze --> Inspect Code --> Inspection Profile
```

From there select import from the select box "manage" besides the current
inspection profile and import the XML downloaded from the link above.

The my profile is ready to analyze Android, JAVA, SCALA, GROOVY and 
Python code. Some more languages will follow - but will also require you
to install plugins. For example for C/C++. As you may see, I do have the
Scala and SBT plugins installed in my dev environment. Which is due to
my side projects in Scala and play. But let's get back to the code
inspection.

Running the inspection with this profile will provide you with a lot of 
findings. The previous [blog post](https://mmiedaner.github.io/reviewing-code-for-fun-and-profit/) gave you some advice how work you 
through an application and basically explains all the points that the 
inspection profiles checks - but that should be check by you as well. 

To show you both profiles in action I did ran them against OWASPs
[WebGoat](https://github.com/WebGoat/WebGoat.git) and here are the
results:

# Analysing WebGoat

|              | **Without test resources** |      | **With test resources** |
| ------------ | --------------------------:| :--: | -----------------------:|
| Error        |                       5883 |      |                    6180 | 
| Warning      |                       5726 |      |                    6003 |
| Weak Warning |                       2375 |      |                    2503 |
| Info         |                        541 |      |                     579 |
| Typo         |                       7902 |      |                    7918 |
| ------------ | --------------------------:| :--: | -----------------------:|
| **Total**    |                  **22427** |      |               **23183** |


Go and try it yourself - let me know what you think of it.
Cheers!
