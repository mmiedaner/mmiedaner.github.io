---
layout: post
title: "Fast As The Flintstones"
date: "2016-06-30 10:18:29 +0200"
category: blog 
link:
filename:
thumbnail:
---
The Flintstones always remind me that you can find some very old framework
in nearly every application. A couple of times I stumbled on Velocity
during penetration tests and so I thought about blowing off the dust
from this "stone age" framework and point out a few things to take care
of with respect to security. 


How does velocity work?
It is a simple as this:

```java
1 VelocityEngine vengine = new VelocityEngine();
2 vengine.setProperty("file.resource.loader.path","templates");
3 vengine.init();
4
5 Context context = new VelocityContext();
6 context.add("order",order);
7 context.add("contact",contact);
8
9 Template template = vengine.getTemplate("inputfile.vm");
10 StringWriter writer = new StringWriter();
11 template.merge(context,writer);
12 String result = writer.toString();
```

Create a template file  - we call it "inputfile.vm" for simplicity.
This file includes the basic text as well as placeholders, which will
be replaced by the velocity engine instantiated in line 3. To substitute
your placeholders with meaningful content you need a context object 
filled with key-value pairs. Finally you create a writer object, hand it
to the template file together with the context and get your complete 
text back (see line 11) - pretty straight forward isn't it?

But with great power comes great responsibility. The most common security
thread associated with velocity is Cross Site Scripting. Since the write in 
the example above simply replaces all places holders with the values based 
on the assigned key, you can easily inject Code (HTML, JavaScript in the 
case of HTML-Mails or web sites) into the templates. So, all you need to 
do is modify the template file ("inputfile.vm") in our example to ensure 
escaping of all parameter values by using the [escape tool](https://velocity.apache.org/tools/2.0/apidocs/org/apache/velocity/tools/generic/EscapeTool.html). 
This comes build in with the velocity framework. Besides HTML, it is also 
capable of escaping XML, JAVA, JavaScript, Velocity itself - which I will 
cover later and of course SQL. Its usage is simple. Within the template file
you need to surround our place holders as follows:

```java
$esc.html($place_holder)
```

And put the following into the tools configuration (tools.xml) of your 
velocity engine:

```xml
1  <tools>
2    <toolbox scope="application">
3      <tool class="org.apache.velocity.tools.generic.EscapeTool"/>
4    </toolbox>
5  </tools>
```

Escaping velocity is also a very important point. If you can inject 
velocity code as parameter value it is basically game over.
Besides setting up endless loops and causing a denial of service you 
may as well start to instantiate Java classes like this:

```javascript	
#set ($fileclass = $customer.Class.forName("java.io.File"))
```

Thereby I assumed that $customer is already an object being passed to 
the template. With a view more steps your up and running all over the 
file system to read or create new files. Clearly - that's something 
you do not want to happen :)

In conclusion, velocity is a nice, slightly old templating framework. 
It can be used safely as long as you do not trust any values within the 
context. In an ideal approach you would validate every value before 
adding it to the context and escaping it when rendering the template. 
Keep it simple - keep it clean!

Cheers :)
