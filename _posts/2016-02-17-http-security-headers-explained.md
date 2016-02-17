---
layout: post
title: "Http Security Headers explained"
date: "2016-02-17 17:07:01 +0100"
category: blog
link:
filename:
thumbnail:
---
Web sites are everywhere and get powned within seconds. Http headers 
will not protect you against rudimentary flaws within the code of your 
side. However they serve two purposes. They add an extra level of 
security to your side on two levels: technical and psychological.
While the technical may seem more appealing at a first glance, the 
psychological carries even weight. Most script kiddies are looking for 
the low hanging fruits. By employing Http security headers on your
site you show that you care about good programming hygiene which implies 
that your side may be programmed very carefully and with security in mind 
as well. Just remember the sign at your neighbor's door warning you about
the (tiny, lovely, always in a mood to  . . .) dog. 


So what am I talking about? There are six headers to care about: 


Strict-Transport-Security	
-------------------------
You already serve your site via https? Why not tell the browser of your 
visitors to enforce TLS on any communication with you? Besides this header 
also protects your visitors against SSL-Man-In-The-Middle attacks.
It should look as follows:


	 Strict-Transport-Security: max-age=31536000; includeSubDomains


It has been specified within [RFC 6797](https://tools.ietf.org/html/rfc6797). 
You may find additional information from OWASP
[here](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security).



Content-Security-Policy	
-----------------------
This is a rather complex header that offers you various protections. 
The full documentation can be found [here]( https://w3c.github.io/webappsec/specs/content-security-policy/)
On the one hand you can specify which sources you include may execute 
scripts or load additional content. You may as well control if your side 
should be embeddable within an iFrame. So it offers a protection against 
clickjacking as well. In this case it should look like this:


	Content-Security-Policy: frame-ancestors 'none'


Besides frame-ancestors you should as well take a look at these options:

* default-src
* sandbox (read more on my post about [iFrames](/iframes/) )
* report-uri

The default-src options allows you to restrict where your site can load 
resources like images, css, fonts or scripts from. Report-uri is a very 
interesting option. It specifies where the browser visiting your site 
should report policy violations to. Clearly this means you need to implement 
more code - but it may be worth it. You will find additional information about 
Content-Security-Policy headers at 
[OWASP](https://www.owasp.org/index.php/Content_Security_Policy_Cheat_Sheet).


Public-Key-Pins	
---------------
Public-Key Pinning was first introduced by [RFC 7469](https://tools.ietf.org/html/rfc7469).
It offers you the possibility to send the hash of your certificate as well as
a max-age information. With these two the client, a.k.a. browser is able to verify
that the certificate received is:

a) the certificate it should expect to receive from you

b) still valid independent of its expiry date and the certificate authority

An example for this header looks as follows:


	Public-Key-Pins:
       	pin-sha256="d6qzRu9zOECb90Uez27xWltNsj0e1Md7GkYYkVoZWmM=";
       	pin-sha256="E9CZ9INDbd+2eRQozYqqbQ2yXLVKB9+xcprMF+44U1g=";
       	pin-sha256="LPJNul+wow4m6DsqxbninhsWHlwfp0JecwQzYpOLmCQ=";
       	max-age=10000; includeSubDomains; report-uri="my-domain.com"


Like the content-security-policy header you can specify a report-uri to 
receive information about browsers encountering problems while validating
your certificate. 

Certificate authorities (CA) had some really bad press during the last years. By
delivering a checksum for your certificate you partially mitigate a 
compromised CA. Still the person visiting your site has to trust you - however
she is now able to verify that the received certificate is the intended one.
And as you already expected OWASP has a [cheat-sheet](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning) 
for this header as well.


X-Frame-Options	
---------------
The x-frame-options allows you to ensure that your page cannot be
embedded into an iFrame and thereby stops clickjacking attacks. The default
setting for this is:


	X-Frame-Options: SAMEORIGIN 


Clearly, x-frame-options are not the only header to avoid clickjacking and
it is not implemented in all browsers. You should combine it with the 
content-security-policy header. For more details check
out the OWASP clickjacking [article](https://www.owasp.org/index.php/Clickjacking).


X-XSS-Protection	
----------------
Modern browsers do bring their own xss-protection. Clearly, it is far from perfect - but
still better than nothing. So, I recommend you set this header as well:


	X-XSS-Protection: 1; mode=block


For more information on anti-xss mechanisms see the OWASP [cheat-sheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet).


X-Content-Type-Options	
----------------------
X-Content-Type and X-Content-Type-Options are two interesting headers. They tell the
browser how to interpret the received file / content. By mislabelling you can get very
interesting results - e.g. "code" gets executed that is actually not meant to be code :)
Anyhow please do always set these two headers correctly. For the X-Content-Type-Options
you should use:


	X-Content-Type-Options: nosniff


This will stop any browser from trying to guess the content-type of a response. Thereby
you will reduce the effectiveness of drive-by-downloads as well as unwanted code execution.
For more information on content-type headers take a look at Microsoft's [page](https://blogs.msdn.microsoft.com/ie/2008/09/02/ie8-security-part-vi-beta-2-update/).



Finally, I stumbled about three pages that may be of interest to you:

* caniuse.com - see what browser in which version has implemented which header. Go to: [http://caniuse.com](http://caniuse.com) 
* securityheaders.io - you may be aware of Qualys and their SSL-Labs. There is a new site similar to it and fully dedicated to HTTP-Headers: [https://securityheaders.io](https://securityheaders.io)
* owasp.org - they offer a nice short write-up on http security headers [here](https://www.owasp.org/index.php/List_of_useful_HTTP_headers).


So, to keep it sweet an simple: Set these http headers!!


Cheers :)
