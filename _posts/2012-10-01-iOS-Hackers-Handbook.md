---
layout: post
title: Charlie Miller - The iOS Hackers Handbook
category: bookreview
---

Charlie Millers Book ["The iOS Hackers Handbook"](http://www.amazon.com/iOS-Hackers-Handbook-Charles-Miller/dp/1118204123/ref=sr_1_1?ie=UTF8&qid=1428952099&sr=8-1&keywords=iOS+hackers+handbook) 
contains what you expect it to.
It is a very rigorous guide on how to look for security flaws and vulnerabilities
within the iOS 1.4 at time I was reading it.

However this actually does not matter that much since the main part of the book
focusses on the principles of how to reverse engineer and how to break iOS. Thereby
Charlie Miller covers various protection mechanisms mobile operating systems offer
today. For example the encryption scheme of the iOS devices being based on two separate
keys. One is derived from the users PIN, if configured, while the other one is directly 
"burned" into the chip set of the device. Based on these two keys further keys are generated
which will be used to encrypt the data on the storage device. Within this chapter the author
as well discusses the different possibilities to secure access to locally stored files. So
one may choose to leave files encrypted only by the basic file system encryption or to 
increase that level by using an application specific encryption on top. In addition the 
programmer can control at which point in time the decryption of the data should take place.
Either when the phone get's unlocked or when the application is started by the user or finally
all the time, when the phone is running.

But there are additional interesting security mechanisms within iOS. Charlie Miller discusses
in great length how the allocation of memory is done. Especially within a web browser this
can be vary complex to secure - just remember that JavaScript has to be executed dynamically
for a good web experience. The iOS Hackers Handbook describes how the allocation
process can be abused and how a technique called "objects with wholes" and return oriented
programming can be combined to jail break the phone. "Object with wholes" is a very interesting
technique where you basically allocate memory parts and in a second step deallocated a smaller
part of that again. Finally the freshly freed memory can be filled with code again that has 
absolutely no logical or pro grammatical connection to its surroundings. Such an approach
within memory that needs to be dynamically allocated and must allow execution of code gives
you an interesting point to start return orientated exploitation - and all because JavaScript
has to be executable from within the browser ;)

In a later chapter attacks against the GSM-Chip are presented and discussed further. However 
such an attack requires way more effort than simply cracking a four digit pin which is commonly
used to prevent unintended use of the iPhone. He also discusses the SDK routines used to
do the authentication. Interestingly the counter of false inputs is not increased during
this brute force attack. Which allows to crack the four digit pin in less than 15 minutes on
a regular iPhone 4. This chapter as well mentions that in the case when the phone should be 
wiped it actually is not. Only the keys needed to encrypt / decrypt the data stored on it
will be removed. I wonder if there could be a way to recover or better regenerate the keys
previously used. With these at hand it should be possible to decrypt the former content of the
phone. Also I am kind of reminded of the old days of MSDOS where you could restore formerly
deleted files by recreating the file index table from the binary data on the disk directly.
Just curious if this would be possible on an iOS as well.


<iframe type="text/html" width="100%" height="550" frameborder="0" allowfullscreen style="max-width:100%" src="https://lesen.amazon.de/kp/card?asin=B00888KNL2&asin=B00888KNL2&preview=inline&linkCode=kpe&ref_=cm_sw_r_kb_dp_a--GxbXWEAEW9" ></iframe>
