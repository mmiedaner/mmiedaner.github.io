---
layout: post
title: "Code Stylometry is not about styling - it is about you!"
date: "2016-03-17 18:21:34 +0100"
category: blog
link:
filename:
thumbnail:
---
Have you seen [Bruce Schneiers](https://www.schneier.com/blog/archives/2016/01/de-anonymizing_.html) post in January this year about deanonymizing
programmers by their style of writing code? Within this post he talks
about two papers which show approaches to tell apart 20 programmers with an
 accuracy of well over 95%. The same researchers are not only capable of 
doing this on source code [[paper](https://www.princeton.edu/~aylinc/papers/caliskan-islam_deanonymizing.pdf)], 
but as well on binary artefacts [[paper](https://www.princeton.edu/~aylinc/papers/caliskan-islam_when.pdf)].


[JStylo](https://psal.cs.drexel.edu/index.php/Main_Page) is an other
approach in determining who is the author of a certain set of words. This
tool is not specialized on source code, but on normal posts like this. 
Interestingly enough, the creators of JStylo released an other tool as well
to disguise your authorship.


So far, I did not come across a comparison of them. This surprises me, 
because looking at the current rise of maleware, crypto-ransomware or 
advanced persistent threats I would have expected a stronger focus on
how to build foundations for accusations. This may be partially related
to the amount of code or text that is required for the analysis. But 
looking at the [malware analysis](http://www.ioactive.com/pdfs/ZeusSpyEyeBankingTrojanAnalysis.pdf) from IOActive - they report several
kilo-bytes for various malware samples. So this may not hold. In addition, 
as Caliskan-Islam et al. pointed out optimizations and similar treatments 
compilers apply to source code barely influence the accuracy of the results.
Even obfuscation does not seem to be a valid protection against their 
approach. But as it turns out, other ways were chosen to justify 
attribution. 


I am currently wondering how one could use these tools in other situations:

* Could you recognize an attacker based on the payloads and attacks she is 
executing? Combining this with the information available through a SIEM or 
log management solution it may as well be possible to differentiate various
attackers. 


* For sure it should be possible to estimate the likelihood of an
insider attack from E-Mail and chat communications of your employees. 


* What about detecting SPAM and Phishing E-Mails based on the way they 
were written?


* Finally - and this is far fetched - such tools could one day also help
you to prove your authorship in court?


However with great power comes great responsibility. What are the ethics
for using such tools and approaches? Let me know what you think.

Cheers! 
