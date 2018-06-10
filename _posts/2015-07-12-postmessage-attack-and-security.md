---
layout: post
title: "PostMessage Attack and Security"
date: "2015-07-12 16:59:53 +0200"
category: blog
---

Based on the [research paper](https://www.cs.utexas.edu/~shmat/shmat_ndss13postman.pdf) by Sooel Son and Vitaly Shmatikov from University 
of Texas at Austin or this slightly older one from 
[Stanford](http://seclab.stanford.edu/websec/frames/post-message.pdf) 
I started playing with Iframes and the HTML5 postMessage function. 
What is postMessage actually for? Imagine the following simplified 
scenario: You are a web developer and your current application 
consists of two iFrames. Both frames should be shown side by side, 
but the first frame normally should take up approximately two thirds
of the available space. So far not to complex to be solved statically.
However if your application now shall be embedded within various other
sides and the aspect ratio of your frames shall shift accordingly to
the behaviour of the user on the main side you will need some communication
between your frames and the main side. And here we are -- in HTML5 
postMessage is used to send message from one iFrame to another. In our 
scenario the main page would send some information for rescaling to your 
application, which would change the ratio of both of its iFrames once it 
received such a message. Very nice - but where is the problem?


One the one hand you may need to verify the origin of the message, which
is quite tricky as we will discuss later. On the other hand you must ensure
that the received message does modify your application in an unwanted
manner - or in short: You need to avoid XSS while you include 
uncontrolled code.
Modern browsers already enforce some restriction like you hardly can 
exchange message between iFrames which have different protocols in 
their src-attributes: http vs. https. 
Also the iFrame sandbox may help you to control the actions that can 
be performed by the included content. However this limitations may as 
well render the included content useless.
[Son and Shmatikov](https://www.cs.utexas.edu/~shmat/shmat_ndss13postman.pdf) 
propose to include a key as URL parameter like an anti cross site request
forgery token within the src-attribute of the embedded frame. This means 
only the parent should be able to know this key and the embedded child 
can extract it from its own URL. However, this approach works in a very 
limited scenario: Only when you embed one child in one parent. Once you 
have various frames from different origins incorporated into your site 
the key would be available to other frames as well - unless you employ 
sandboxing.

Validating the origin of each message strictly might be an additional 
helpful step. This implies that scripts can be executed as well that no 
additional event handlers can be registered. In the later case the 
embedded child 
frame could register an evil onMessage event handler to another frame or
its parent.   

As you see - not a trivial problem. However do consider that an possible
attack page may include your page twice (or even more). In such case the
attack page could bypass the origin validation by:


`var attackWindow = $('#victimFrame2').get(0).contentWindow;`

`attackWindow.postMessage('evil message', 'victim url');`


Anyhow - having explained the problem. To demonstrate such a situation to
developers as well as management I created "PMAT" - a Post Message Attack 
Tool. It can be obtained from 
[here](https://github.com/mmiedaner/security/tree/master/pmat). It is a 
very simple and basic web page to allow you to load up to two frames - 
a victim frame and an attack frame. You may as well configure a message 
to be send to the victim frame. The message can be send from the page it 
self (hidden iFrame with the same origin as the page) or from a custom 
loaded attack frame. Besides the custom loaded attack frame may as well 
include code to send messages to the victim frame.

Enjoy!
