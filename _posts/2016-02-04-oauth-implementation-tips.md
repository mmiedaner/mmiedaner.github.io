---
layout: post
title: "OAuth Implementation Tips"
date: "2016-02-04 20:35:14 +0100"
category: blog
link:
filename:
thumbnail:
---

The OAuth protocol has been around now for some time. It get heavily 
deployed within mobile apps and web applications that “mash up” other 
services. REST based web services also rely on it. To summarize it at 
a high level. [OAuth](https://tools.ietf.org/html/rfc6749) is a token 
based protocol. Most implementation mix authentication and authorization in 
different percentages - so it is hard to label OAuth as strictly as 
either an authentication or an authorization protocol. It offers different 
workflows depending on the scenario you like to use it in.

Within this post I would like to focus on its usage scenario within mobile 
apps. So we are talking about you as the resource owner as well as the app
developer - you offer a service and different mobile app to use it. What 
happens is:

- The app requests access to your service without any authentication token - first call.
- You redirect the app to an identity provider choose either by you or the user via your front end.
- The user authenticates at the identity provider of choice and redirects to you for further steps.
- You provide the app with a code (min. 6 chars).
- This code is only valid for a short time and has to be returned to the identity provider - aka you.
- After you received the code from the app again, you will issues two tokens signed with a secret.
- One token is short lived - the so called access token.
- One token is long lived - the so called refresh token.
- The app calls you again with the access token.
- Based on the validity of the access token you grant access to certain resources.

So, that is basically it on the web as well as mobile side. Other flows or so called “grants" are simpler and do not use a refresh token. They only provide you with an access token and will not be discussed further in this blog post. This is mainly because their weak point is the token storage as discussed further below.

But let’s get back to the original topic. During the last years I review the source code of various apps and web applications employing OAuth. What I would like to share are common mistakes I found:

### Insecure Token storage
Yeah, this is a common and an easy one. OWASP complained for a long time about the insecure storage of credentials. And that is absolutely the same for access and refresh tokens. Especially in mobile apps the tokens get often put directly onto the file system. Doing this, they are stored within the container of the application. This offers you some very weak protection assuming that you run on a non jail broken / rooted phone without any malware or malicious app. I would not bet on these conditions for my customers. So - at least, put the token in the key-chain or an equivalent storage location protected by the mobile OS. And again - sorry, storing the tokens encrypted within the container of the app is no acceptable solution. Why? Where do you put the key for encrypting and decrypting the tokens? Right - in the source code, which no one will ever decompile. Do not do this - come on!

### Insecure URLSchemes or Intends
As pointed out above in step 5 at one point the app receives a redirect to an url specified by the app with a parameter called code. This various digits / characters have to be returned to the token issuing side within a short period of time. Within iOS you can simply bind this URL to your delegate which handles the code and sends it back to receive the tokens. On Android you may use an Intend to transport the code to the component or class that handles the OAuth-API calls. In both cases you have to find a way that no malicious app can intercept the code and cache it into tokens. Be creative - this is not simple and the parameter “state” specified within the [RFC](https://tools.ietf.org/html/rfc6749) may offer some protection, but it is not bullet proof. So restrict this interaction as much as you can.

### URL Verification / Pinning
Although it is to some extend against the idea of OAuth - did you consider URL pinning or hardcoding? That means on the token issuing side the return URLs including the code must be the same as the one that receives the tokens and has to be pre registered with the token issuing side as well. This clearly causes some unintended overhead - but helps you as an identity and / or resource provider to ensure the token exchange even further. On the other hand the parameter state has to be returned from the token-issuing side. So you may consider to preregister different values for this parameter for different steps of the process. Clearly this requires that the token-issuing as well as the token-requesting side do need to check them constantly. This offers only a very limited protection, since after decompilation of the mobile app or sniffing the handshake these “state” parameters would be known to the attacker. A one time pad used for this parameter would be nice - but this is out of the scope of the RFC.


Finally preregistered URLs are as well important for the token refresh calls. This means before the short-lifed token expires the app calls to renew the access token. It thereby receives a new pair of tokens: access and refresh. For this exchange the callback url for the tokens should as well be specified in advance to avoid that the token pair ends up with an unintended application.

### Password reset
Password reset of the user account may not always be within the scope directly. However, imaging the following scenario: Besides your web based application (username / password for authentication) you offer as well an application that is based on OAuth 2.0. So you provide the tokens, the resources and all the applications. Actually a perfect scenario of full control. However there is one little thing you should take good care of. Once a user resets it password, locks his account or for any other reason an account gets locked - you do need to invalidate all tokens issued for this account. Otherwise your service could be used with the tokens but not with username and password as credentials.

### One Credentials for all
Also this is a bit far fetched - however using the same secret for signing the tokens for all OAuth clients is not a good idea. I strongly recommend to use a separated secret for each client. Handle these secrets like password - extremely carefully.


So far my adventure in reviewing OAuth based code. Hope you get something out of it. What is your opinion? Did you encounter different security problems? Let me know.

Cheers!


