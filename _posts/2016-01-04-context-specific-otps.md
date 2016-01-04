---
layout: post
title: "Context specific OTPs"
date: "2016-01-04 13:28:49 +0100"
category: blog
---
One time passwords are mainly based on two triggers - either 
time or a counter of events. Combined with a pre-shared secret 
you can build an OTP-Generator like Google-Authenticator. 
Both ways (time or counter) you do not have any context within 
the generated one time password will be generated. As an example 
that I will return to within this blog post I pick online banking.
During an online banking transaction you normally enter the amount
of money you would like to transfer and finally receive an OTP via
some second channel - e.g. SMS and thereby secure your transaction.
But which connection exists between the characters or 
numbers send to you via a second channel to the amount of money 
you would like to transfer? - Yeah, none. And this is what I would
like to talk a little bit more in detail. What ways exist to combine
the context in which you are with OTP you are going to receive. 
So let’s get to it at a more technical level:


Google Authenticator is based on a shortened HMAC of the current 
time stamp and a pre-shared key. Mostly the first 8 bytes of the 
HMAC are used. Such an approach relies on two things:

a) you have approximately the same time on both your mobile device 
as well as the server you are interacting with.

b) you employ a pre-shared key that has not yet been compromised.


This approach can hardly be extended to be context sensitive unless 
you do integrated it on the users side within the client. This makes
you a primary target for reverse engineering and since you have no real
separate second channel you do weaken the authentication. However, such
an approach may still be better than no additional security at all. I
still do not recommend it.


However if you do compute the one time pad on the server side and 
than transmit it to the user via a second channel it is quite easy. 
You do have all the information you would like to integrate into the 
password generator. Let return to the online banking example - simply 
concatenate the amount of money that should be transferred with the 
time stamp and determine it HMAC.


So what else could be combine with the time stamp? Yep - the session-id. 
Compared to a short range of characters (letters and or numbers) you 
have about 128 bit entropy normally. On the other hand I like to 
recommend you change the session-id after receiving the one time pad.


An interesting way to bind an OTP to an users context is to analyze 
and record her behavior while using the application. For example you 
keep an numeric value within the session to indicate the likelihood 
that the user is the one she claims to be. Every action she performs 
increases or decreases this value depending if the preformed action 
correlates with previously recorded behaviour. Examples for this 
are typing speed on input fields, reading speed per page and so on. 
However combining such a numerical indicator with a time stamp and 
an other value representing the context of the transaction is a 
nice approach to create a context specific one time password.

Cheers!
