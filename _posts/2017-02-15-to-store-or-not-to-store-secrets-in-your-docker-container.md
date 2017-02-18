---
layout: post
title: "To Store Or Not To Store Secrets In Your Docker Container"
date: "2017-02-15 09:17:23 +0100"
category: blog
link:
filename:
thumbnail:
---
Docker containers are an easy and in many cases more secure approach
to establishing an flexible and even agile production environment. The
community around this products now starts to solve and old problem
of every production installation of any software. Where and how do you
store or better manage credentials - even privileged credentials?


On a classical JBoss application server you were left with picket-box for
quite a long time. Unfortunately this library is completely open source
and more of a proof of concept implementation. Since its security is 
based on a hard coded key you need to modify this library and compile it
manually to achieve a decent level of security. However, you still can
loose all credentials once an attacker could copy your application.
In a docker environment you face such a scenario with every application.
Docker swarm now offers you a key management solution based on the 
least-privilege principle. This means that every container can only 
access those secret it ultimately needs and nothing more. In comparison with
Kubernetes this is a big plus for docker swarm.


There are other approaches to this problem as well. Take a closer look at
the [Amazon Key Management Service](http://searchaws.techtarget.com/definition/AWS-Key-Management-Service-AWS-KMS). Rumours say that Google, as well,
is working on a closed source tool for Kubernetes. In addition you may 
employ [Red Hat's OpenShift](https://docs.openshift.com/container-platform/3.3/dev_guide/secrets.html) to manage all secrets on top of Kubernetes.


Finally [HashiCorp's Vault](https://www.vaultproject.io/) seems to be a very good solution. Still it lacks
native support within docker. On the other hand this is an advantage. It
enables you to use it with and without docker. So you could set up a central
place to manage all credentials. Since HashiCorp's Vault was created with
industry standards and regulations in mind you encounter features like
key rotation, audit logging, siem integration and so on within this product.


Runtime application security and docker seem not to be the best friends
in the sense that there are only two products available: Twistlock and
Aqua Security. You may take a closer look at them or try to implement 
runtime application security within your application (inside the JRE or
any other runtime your code needs).


In conclusion we need to find a way to ensure that we either do not ship
any credentials with our containers or that we ship them safely. The latter
normally implies additional infrastructure for the management of the
secrets. The nice thing about docker containers is that you can validate
them and security aspects any time. There is even a [CIS Benchmark](
https://benchmarks.cisecurity.org/tools2/docker/CIS_Docker_1.12.0_Benchmark_v1.0.0.pdf) for hardening docker containers. Reading the document turns 
out to be time consuming since it has quite a few pages. However, what 
would be a guide line without a script checking it's implementation. 
You'll find the script [here](https://github.com/docker/docker-bench-security).


So, what now? To summarize this post, there are several ways to handle the
management and even storage of keys and credentials within a docker 
container safely. Depending on the risk your application poses to your 
company you may choose a different one. But always keep in mind that 
storing and shipping secrets within a container to public places 
(docker hub, github etc.) is not a good idea.


Cheers!
