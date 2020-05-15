---
layout: post
title: "WAFalyzer"
date: "2020-05-15 10:47:11 +0200"
category: blog
link:
filename:
thumbnail:
---
WAFalyzer is a small python script I wrote due to the need of analysing
requests captured by a F5 BIG IP Web Application Firewall. This analysis 
was more related to traffic as to security, but I thought it would be good 
to share the script. 

## What does it do? 
It assumes that you exported all
requests into one folder from which it imports all the files and parses
them for URL, time stamp, request size and response code. Thereby it offers
you the possibility to bundle or group URLs based on path parameters. This
comes in handy when you have a REST API. In such case the URLs often end
with the id of the object in question. So you end up with a huge amount
of different URLs which all relate to basically one web services.


## How do I use it?
It is a command line tool, so open your shell and make sure your python is
installed and up to date:
```bash
python --version
```
The script takes up to four parameters. The first is: --sDir. With that 
you specify the directory the script should look for the exported requests.
With --output you give it the file name into which the data should be
exported. --merge tells the script which URLs to group. Thereby you only
need to give the common part of the URL or a piece of it. Finally with --analysis you can specify three types of analysis:

* Simple - Just URLs and count of requests found for this URL
* AddAverage - Like Simple, but you get the average request size as well
* ALL - Full blown analysis with response codes, requests sizes and various statistical data

Note that the --analysis is optional. Its default value is "All"
 
So the final call could look like this:
```bash
python WAFalyzer.py --sDir /home/john/f5-export/*.html --output WAFReport --merge sync log --analysis All
```

And that's it - hope you have fun with it. The script can be found [here](https://github.com/mmiedaner/security/tree/master/WAFalyzer).


Cheers !

