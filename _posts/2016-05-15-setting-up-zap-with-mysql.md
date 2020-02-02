---
layout: post
title: "Setting up ZAP with MySQL"
date: "2016-05-15 20:09:23 +0100"
category: blog
link:
filename:
thumbnail:
---
Have you being using ZAP - OWASP's ZAProxy? It is an intercepting
proxy combined with a fuzzer, a vuln-scanner and many other 
features that come in very handy, when you are into analysing and
testing web, mobile or any other application that uses HTTP as
a communication protocol. The only alternative to it, that is
recommended all over the place, is the BURP Suite. However during
the last years ZAP grew up fast and is now completely even to BURP
Suite. Clearly, both have their pros and cons, but at the end of the
day the difference between the two is melting away.


Within this blog post I would like to show you how to hook up
ZAP with a MySQL database. Simply because ZAP is using HSQL out of 
the box, which may cause some headache from time to time. For example
the file size limit of your operating system gets reached or the
HSQL DB crashes. The default setup of ZAP works in most cases, but once
you start using ZAP as an automated scanner - maybe even triggered
by your Jenkins or any other build server - you need a reliable database
as a back end. Unfortunately I haven't found a good description on how
to do it - so I decided to write this post.


Fire up your Kali installation and do the following steps: First
go to /etc/mysql and find out how to access the local MySQL database
by catting the file called debian.cnf. Here you will find the username
and the password for the maintenance user. Now connect to the database
with this user by issuing the following command:

```bash
mysql -u debian-sys-maint --password=<the password from the file>
```

or simply - if you are in the sudoers-group:

```bash
sudo mysql
```

Now you need to connect to the right database by:

```bash
mysql> connect mysql
```

To add a new user issue this command and set his password as you like:
```sql
CREATE USER 'zap'@'localhost' IDENTIFIED BY '<zaps password>';
```

Once the user exists, we need a database for this user:
```sql
CREATE DATABASE zaproxy;
```

OK - so far so good. The zap user now needs to be able to access the 
zaproxy database. You do this by granting him all rights on the database:

```sql
GRANT ALL PRIVILEGES ON zaproxy.* to 'zap'@'localhost';
FLUSH PRIVILEGES;
quit;
```

With the "flush privileges" command you fixate the rights of the user and
with the "quit" command you return to your command shell. Now reconnect
to the zaproxy database as zap by:

```bash
mysql -u zap --password=<zap's password>
connect zaproxy;
```

At /user/share/zaproxy/db you will find to files:

* mysql.properties
* mysql.schema

Take a look inside MySQL.schema to find the SQL statements to create the 
necessary queries and copy them to the MySQL prompt you just created. So 
finally ZAP needs to know that it is supposed to use the MySQL database. 
Therefore uncomment and edit the following lines from the config file 
"db.properties" within the same directory to like this:

```bash
db.class	= org.zaproxy.zap.db.sql.SqlDatabase
db.type		= mysql
db.driver	= com.mysql.jdbc.Driver
db.url		= jdbc:mysql://localhost/zaproxy
db.user		= zap
db.password	= <zap's password>
```

By the way - make sure that you commented out the lines above - those
to disable the use of HSQL databases. Before you can start using ZAP with
this configuration you should ensure that the MySQL driver for java
exists either via
```bash	
apt-get install libmysql-java
```
and copying it from this place afterwards:

```bash
/usr/share/maven-repo/mysql/mysql-connector-java/5.1.38/mysql-connector-java-5.1.38.jar
```

Or download the appropriate jar from ORACLE and place it at:

```bash
/usr/share/zaproxy/lib
```

Now the moment arrives to start zap and watch out for errors....
Do not forget to start zap as this to enforce the use of the MySQL database:

```bash
zap.sh -experimentalDb
```

At a first glance it looks wrong, but is only one "-" in front of
"experimentalDb". And that is all the magic - enjoy and let me know
if you encountered any problems :)

Cheers!
