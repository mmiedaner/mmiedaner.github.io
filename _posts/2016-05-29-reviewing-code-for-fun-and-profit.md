---
layout: post
title: "Reviewing Code For Fun And Profit"
date: "2016-05-29 11:02:54 +0200"
category: blog
link:
filename:
thumbnail:
---
Code review is often called boring and for loosers. However,
depending on how you do it - you may save time and energy which means
more money for less work. Here is how to do it without kicking of a 
static analysis engine: 


Start with the entry
points of data into the application. Find the classes that accept user
input. Here you should check, how they are filtered and validated. A good
application has a strict definition of characters to accept for each 
parameter it exposes. This is one of the easiest steps to avoid injection
attacks.


Once that part of the code is "clean", continue to follow the users input
into what I would like to simplify as the "service layer". Here all data
get interpreted and manipulated to do the applications job. Thereby it
is important to look for a simple and easy to understand logic. If things
get to complicated mistakes start to appear. So make sure, you understand
what is happening and in most cases why. :) If you find code that seems to 
be unused - report it!


And finally take a look at how the data is stored. Is it in a database? Is 
it in a flat file? How are the statements for putting data at rest written?
Is there a possibility to extend the query / paths or somehow alter the
commands?


So, now you made one way through the application from the outside in and it
is time to return to the interfaces again. At this point, follow the data
from their place of rest to the interface and keep in mind that you need
to ensure that presented data is validated and filtered as strictly as
the input accepted. The goal is to ensure, that once you have malicious 
data within your application, it can not cause further damage.


Sensitive data like passwords, payment information and so on are also a
target for many attackers. Follow such information as closely as possible
through the application and ensure that there is no operation that:

- leaks them
- acts on them without authorization checks
- stores them inappropriately 


And now, after following data through the application, it is time to think about
possible errors. How is the error handling implemented? Are all possible
error caught by the exception handling? Is it a consistent approach 
across all layers of the application? How are errors reported to the
user or other services? Can any information be leaked or is even unfiltered
user input transported?

At this point we ensured that the application does a good job. We haven't
spend much time on the users - besides their input. But how is the 
authentication and the authorization implemented? Are they robust? Are
they handled in a consistent way across the whole application?

And finally two more points to check: Take a close look at all
log statements. 

- What data is written to the log adaptor? 
- Should this data be written in this way?

Also developer comments are very helpful - especially comments like TODO
or FIXME often point to incomplete or broken functionality. Some developers
even report the IDs of issues that were found during the testing phases -
double check all code that is close to such comments.


To summarize all of the above - there's a ten step guide to code review:

```
1. Check filtering and validation of all user input
2. Check how user input is handled on the "service layer"
3. Check how data is stored
4. Check how data is returned to the user or any other interface
5. Check how sensitive data is handled
6. Check how errors are caught and handled
7. Check how authorization is enforced
8. Check how authentication is performed
9. Check all logging statements
10. Check for comments like:  TODO or FIXME
```
 
I am curious to hear your thoughts on this topic. Cheers!

