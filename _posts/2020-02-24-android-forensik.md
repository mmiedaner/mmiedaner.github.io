---
layout: post
title: "Android Forensik"
date: "2020-02-24 07:57:22 +0100"
category: bookreview
link:
filename:
thumbnail:
---


This blog post is kind of special since I am writing about book that I 
actually read in German and not in its original language. Andrew Hoog 
wrote his book ["Android Forensik - Datenrecherche, Analyse und mobile 
Sicherheit bei Android"](https://www.amazon.de/Android-Forensik-Andrew-Hoog/dp/3645602100/ref=sr_1_1?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&keywords=Andrew+Hoog+android+forensik&qid=1582549160&sr=8-1) in 2012. It got published by FRANZIS and provides
you with a sophisticated introduction into forensics as well as broad 
overview of the commonly used tools. Also this book has been written
some time ago and many versions of Android passed, it is still a valid and
important resource. The basic principles stayed the same especially, if
it comes to the file systems. And this is the point Andrew Hoog starts his
book with: file systems and there analysis. Besides their logical structure
he also explains the memory allocation in smart phones. Since the NAND
memory works on pages which can be written or erased this gives an important
hint to researchers to reconstruct previous actions on the phone. Besides
YAFFS2 is the common file system which bears its nitty gritty details.
These get explained in greater depth by Andrew Hoogs within the first
chapters. The following parts to the book include the most important 
folders of the android operating system and some useful information about 
its mount points. For example Andrew explains the difference between the 
emulated and the real SD card and how these mechanisms differ between the 
test devices he uses during all chapters of his book. Later on he continues
 to discuss the first steps once a phone
has been received for investigation on how to access the data without 
changing them or at least minimising the impact of the analysis. This
topic get especially tricky depending on the type of smart phone and user
lock implemented (none, pin, pattern, passphrase or biometrics). Andrew
Hoogs discusses the pros and cons of various software as well as hardware
based ways to extract data. This section is followed by list of 
commercial tools available to simplify the process of data extraction.
Along all chapters this book emphasises how to build your own forensic
workstation based on Ubuntu Linux and gives various well documented 
examples one can easily try at home. The last chapters of the book are
dedicated to the analysis of mobile apps. Thereby the author explains the
commonly used files, databases and folder structures of mobile apps. This
section is particular interesting, it also helps a pentester as the
location of sensitive data within the files per app are described.    
All sections are include small example scripts or shell commands that help
the user to manually reproduce the essential parts on their private
smart phones without bricking / destroying them.

In conclusion I do recommend reading this book also the examples given 
within seem to be outdated. It is amazing how much information remained 
valuable since the time of writing.

Cheers!
