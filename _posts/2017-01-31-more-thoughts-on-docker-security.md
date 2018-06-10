---
layout: post
title: "More Thoughts On Docker Security"
date: "2017-01-31 19:28:26 +0100"
category: blog
link:
filename:
thumbnail:
---
The last post described some overall aspects of docker security.
Today I would like to dive a little bit deeper and discuss a few
additional technical aspects. As mentioned in the previous post
docker is based on shared resources especially the kernel. That
implies that you should run a hardened kernel. For example you
should have the 


`CONFIG_SECURITY_SELINUX`


enabled and SELinux should be in enforced mode. Here you will find
out more about [SELinux](https://selinuxproject.org/page/Main_Page).
If you are using a docker verison greater than 1.10 seccomp is 
supported as well. A detailed description about creating a seccomp profile
can be found [here](https://docs.docker.com/engine/security/seccomp/).
Once you created the file you can start your containers like this
to enforce the usage of the profile:


`$ docker run --rm -it --security-opt seccomp=/path/to/seccomp/profile.json hello-world`

The profile is basically a list of system calls that should be available
inside your container. With the help of the _strace_ command you can 
create the profile file. While you will find more information about
the seccomp profiles [here](https://docs.docker.com/engine/security/seccomp/), keep in mind that they are based on the following structure:


`
{
"defaultAction": "SCMP_ACT_ERRNO",
	"archMap": [
		{
			"architecture": "SCMP_ARCH_X86_64",
			"subArchitectures": [
				"SCMP_ARCH_X86",
				"SCMP_ARCH_X32"
			]
		},
		...
	],
	"syscalls": [
		{
			"names": [
				"accept",
				"accept4",
				"access",
				"alarm",
				"alarm",
				"bind",
				"brk",
				...
				"waitid",
				"waitpid",
				"write",
				"writev"
			],
			"action": "SCMP_ACT_ALLOW",
			"args": [],
			"comment": "",
			"includes": {},
			"excludes": {}
		}, . . . 
        ]
 }`

And since we are already in the depth and trenches of Linux security Docker
also provides you the classical application capabilities as on a regular
Linux system. Their details are discussed in this [paper](http://www.usenix.org/events/sec02/full_papers/wright/wright.pdf) 
from 2002 - quite some time ago :). Anyhow these capabilities can further 
reduce the privileges an application has within the container. But keep in 
mind that you can run into inheritance problems as you assign them. The 
man pages of libcap and the libcap-ng-utils will guide you further as well 
as this [article](https://lwn.net/Articles/632520/).


In addition to the hard core Linux security settings there is a simple
step that can be overlooked easily. Normally docker runs as root and
so do the container unless you start them with the _-u_ flag. In general
I recommend that you use a different user for each container.


Service isolation as well as resource limiting are other principles that 
you could employ to harden your docker installation even further. But this
are steps you would take to secure any server in general. In conclusion
there are a lot of steps to take and a lot of options to configure - 
do not get confused and keep it as simple as possible.

Cheers!
