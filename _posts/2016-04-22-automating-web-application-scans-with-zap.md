---
layout: post
title: "Automating Web Application Scans with ZAP"
date: "2016-04-22 17:09:30 +0200"
category: blog
link:
filename:
thumbnail:
---
Automating web application scans - why? Simply to improve
the quality of your product and catch vulnerabilities as early
as possible. There are several tools to do it. You may either use
ZAP, Burp, Nikto or similar suspects. Within this post I
would like to show you how to automate [ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) and integrate it into
your continuous integration / continuous deployment setup. You should
be able to read some python code and have some experience in shell
scripting to get it up and running. Nothing very complicated so.
But, before you grep all necessary [scripts](https://github.com/mmiedaner/security/tree/master/ZAP/automation)
you need to install the python-zap-api client via this command on your 
build server:

`pip install python-owasp-zap-v2.4`

A more detailed howto can be found [here](https://github.com/zaproxy/zaproxy/wiki/ApiPython).

Having said that - let's get started. As a first step create a new 
Jenkins Build Plan. Once everything works you can copy the configuration 
into already existing projects. This build should execute a few shell
commands. The first one is:

`zap.sh -config api.disablekey=true`

You may as well start ZAP in daemon mode. However, I found that my scripts
will not work in such case and that the scanner behaves in strange ways.
So, I do recommend starting it in full blown GUI mode with the command
above. The parameter "-config api.disablekey=true" forces ZAP to accept 
commands via its API without any API-Key. This is OK, if you work in a 
hardened environment and your ZAP daemon can not be reached from out side 
your network. To give ZAP to start up fully add the following line to 
wait 5 seconds:

`sleep 5`

And finally start a script to scan your apps. The script I am using
can be found [here](https://github.com/mmiedaner/security/tree/master/ZAP/automation) including the configuration file it depends on. You
can simply start it:

`python pythonZapRemote.py --config config.json`

This tells the script to load the configuration file "config.json" from
the same directory that it is in. You can as well specify a list of URLs
separated by spaces as follows:

`python pythonZapRemote.py --urls URL1 URL2`

But what does the script do? After creating ZAP session it opens the URL
provided and spiders it. Depending on your configuration it performs an
active vulnerability scan afterward and finally creates a report. At
this point you are free to move the report to a place where your 
developers can access it to improve their code - or simply mail to
them via the unix command line. Do not forget to stop ZAP:

`java -jar zap-api-2.4-v7.jar stop zapaddr=127.0.0.1 zapport=8080`

Ok, so far so good. Now I would like to discuss the various options of
the configuration file.

* sessionPath
-------------
This parameter defines the path where the session file should be 
created.

* reportType
------------
ReportType specifies which format the final report should have. Valid 
options are: 
	* HTML -- for a regular HTML-ZAP-Report
	* XML -- for an XML file containing all the data
	* Custom -- for an HTML Report which is filtered for false positives

* reportDir
----------
This parameter is the path to a directory where all reports should be 
stored in.

* http-proxy and https-proxy
----------------------------
These are experimental parameters. In the next release they will allow
you to specify which port zap should listen on for http and https 
connections to intercept.


* target
--------
This parameter is a list of targets that should be scanned. For each 
target you need to specify:
	* url - the URL at which the application could be reached.
	* sessionName - the name that should be assigned to the session files and the report as well.
	* respider - this parameter tells ZAP to spider the application after the scan once again. It takes the string values "true" or "false".
	* selenium - this parameter is for shell commands, that should be executed before the target gets spidered and scanned. I named it selenium to 
signal you to use this parameter for starting selenium test cases, where the
browser in use should be configured to use ZAP as a proxy.
	* scan - this parameter is true or false as strings to disable the scanner in case you would like to only spider your application.

After the targets you can define a list of false positives that should
be removed from the custom report. This works only for the custom report
and not for HTML or XML.

* falsePositive 
---------------
This parameter is a list of false positives to be removed which are 
described by the following parameters:

	* url - the URL where the finding was discovered.
	* param - the parameter that is potentially vulnerable.
	* evidence - the evidence that ZAP reports for the alert.
	* alert - the alter text it self to match.

And that is basically it. By the way, if you do not use the configuration
file and instead provide a list of URLs as described above, the script 
will create a directory on level up in the directory structure from it 
self a new directory and store session files as well as reports in it. 
Thereby the session and report names are based on a time stamp and the 
numerical value for the position of the URL in the list (0,1,2,3,4, 
and so on).

Finally, you may add a check to break the build if either certain 
vulnerabilities are found or if any at all are found. This is not yet
part of the script, but will be added soon.

And now - happy automated scanning. Automating tools like ZAP helps you 
to find low hanging fruits and simple vulnerabilities.
It is in no way comparable to a real pentest. 

You have suggestions for features, improvements or found a bug? 
Let me know - I would love to extend the script.



Cheers!
