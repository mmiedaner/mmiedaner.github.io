---
layout: post
title: "Tangled Web: A Guide to Securing Modern Web Applications"
date: "2019-07-08 08:41:50 +0200"
category: bookreview
link:
filename:
thumbnail:
---
Tangled Web: A Guide to Securing Modern Web Applications by Michal Zalewski
 is a comprehensive review of the security of web applications. In 
comparison with other works on this topic the author dives in deeper and 
focusses on the http protocol, the html, css, javascript
language consortium and finally browser security itself. These topics are 
rarely covered in the traditional literature recapping the 
[OWASP TOP 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project). 
Interesting aspects, like how various browsers treat the same
origin policy differently by taking different parts of the URL into account
to determine the origin. This has some side effects not only
concerning java script but also involving HTTP-Security Headers like the
X-Frame-Options Header. Since not all browsers support all security headers
you may use the X-Frame-Options and the Content Security Policy Header to 
protect your application against click-jacking. However, since different browsers
define the "origin" differently, you may end up in trouble using "SAMEORIGIN"
within the X-Frame-Options, while specifying multiple domains in the Content
Security Policy Header. Keep in mind, that the origin definition used by the
browser may not include in the protocol - so connecting to an allowed domain
via http may be possible as well.  

An other aspect that was very interesting to me where the chapters on 
browser security. It is quite a challenge to write a secure browser. Reading
these parts of the book makes you as well understand why the browser has
been heavily targeted in iOS jailbreaks and various other attacks on 
computers in general. It is a good target for attackers and for a security
professional as well as a developer a night mare to get right.   


Finally, I have been looking for a write up of how to include foreign 
content into my own applications and pages without opening all doors for
the 3rd party code. Michal Zalewski discusses all aspects of this topic
within a few chapters. Thereby he shows not only the complexity of this
task but also offers a way to do it. He summarizes his advice at the
end of each chapter as a "checklist". An excellent choice which may serve
you as a list of security requirements. 


These are only a few of many topics covered by the author to demonstrate that web 
application security is way more than just cross site scripting, cross site 
request forgery and SQL injection. It is an very interesting and easy to read 
book although not missing the technical depth. Unless you haven't spend some 
time developing web application professionally and some years in the seat as 
a security professional I would not recommend this study to you because of the 
required technical understanding. However once read, I promise you: you
will see your previous decisions in a different light. The web is way more
complex than it seems to be.


Cheers !!


<iframe type="text/html" width="336" height="550" frameborder="0" allowfullscreen style="max-width:100%" src="https://lesen.amazon.de/kp/card?asin=B006FZ3UNI&preview=inline&linkCode=kpe&ref_=cm_sw_r_kb_dp_KMkjDbY1745HJ" ></iframe>
