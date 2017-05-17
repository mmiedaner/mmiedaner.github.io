---
layout: post
title: "Unsecure High Risk Users"
date: "2017-05-02 13:12:43 +0200"
category: blog
link:
filename:
thumbnail:
---
Recently I stumbled upon a paper by John Scott-Railton from Citizen Lab 
in which he discusses a study conducted by him with the help of the
university of Toronto focussing on the security of high risk users. To
be honest I was shocked after reading this document. This paper is worth 
reading - as it points out the fundamental flaws we all have and how we 
fail over and over again. First - what are high risk users in 
Scott-Railtons [paper](https://www.computer.org/csdl/mags/sp/2016/02/msp2016020079.pdf)? He was focussing on civil rights activists, reporters and 
people who are suffering from governmental prosecution. 


As pointed out those guys were heavily target by phishing. A topic I have
been writing about a bit [[1](https://mmiedaner.github.io/phishing-explained/),[2](https://mmiedaner.github.io/feeding-the-phish-part-1),[3](https://mmiedaner.github.io/feed-the-phish-part-2/),[4](https://mmiedaner.github.io/feeding-the-phish-part-iii/)]. As pointed out by Scott-Railton the 
social engineering part of most attacks is sophisticated compared to the
technical attacks. In his paper he shows various analysis of malware
families used with the phishing E-Mails. It is astonishing to see, that
no fancy trojan or zero days have been used. Most malware families have
been used over four to five years. This leads to the conclusion
that the technical expertise of the victims seems to be low and that
updating the system / patching is not done well. 


This lack in technical skills seems to be covered partly by behavioural
measures. This means that instead of increasing the security of their
day to day use computers activists shifted to use file sharing services
like Google Docs instead of sending documents via E-Mail. This somehow
protects against phishing scams and malware - but it also puts the users
at risk, as Google still records a lot of data about them.


An other point Scott-Railton discusses at great length is the lack of
two factor authentication. In principle I agree with him. However I would
like to argue that if you do not have the time to patch - do you really
expect the use of multi factor authentication? The MFA concept is harder
to grasp and to use than patching.  


This brings us to the final question - who is responsible? High risk
users can face dramatic consequences. However, as a provider of a 
service platform your time is limited, so you can not secure it to the
last bit. Scott-Railton propose to enable multi factor authentication
by default. This could be an option - but you, as platform owner, still
need some motivation to enforce it on your users and maybe suffer
from the loss of customers. Yeah a bitter pill to swallow. If legislation
as proposed in the paper is really a good solution is up for discussion.
I do not agree on this point. There should be an other motivation. What do
you think?

Cheers !



