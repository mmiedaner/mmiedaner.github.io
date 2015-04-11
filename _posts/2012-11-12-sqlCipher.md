---
layout: post
title: Secure Data storage on iOS-Devices with SQLCipher
category: blog
---

Secure data storage on mobile devices 
is the most common thread today. This 
problem is not limited to iOS. It 
affects android as well. Considering 
jail-broken devices it becomes even 
more evident, that the developer should 
take good care in implementing client 
site storage mechanisms that reach 
beyond the offers by the sandbox. The 
latter will fall apart once your device 
is jail-broken. Clearly modern mobile 
operating systems offer great protection 
features - however unused or not implemented 
correctly these measures are worthless.


[SQLCipher](http://sqlcipher.net/) offers a great way to avoid 
this thread. It offers strong cryptography 
and high performance. Both required in the 
case we look at. In addition it allows you 
use the most common database on mobile 
devices: SQLITE. The use of SQLCipher is 
nearly transparent for the app. Only the key 
needs to be set, after opening the database.


Now let's assume we do have an application 
based on SQLCipher. Somehow we got our hands 
on the database file (Jailbreak, Backup Extraction, 
Code Injection,....). How can we attack the 
recovered file?
Brute force - simple but very time consuming? 
Really? We obtained the database of a mobile 
application. Let's assume that the user has 
control over the key used to encrypt the DB 
and needs to enter it on a mobile device. 
This means the key won't be that long, since 
you have type it every time you open the app. 
For safety let's assume the max will be 8 
alphanumeric characters. This sheds some small 
light on the idea to brute force the key.


Here's how I went about it: First I started to 
create databases with the "-init" command of 
SQLite. This command allows you to create a 
command list that will be execute step by step 
when opening a database file. The command:


sqlite3 -init initDBwith4DigitPin crypotest.db


will result in a sqlite3 database encrypted 
by a four digit pin. The file initDBwith4DigitPin 
included the following:


	PRAGMA KEY=1234;
	create table t1(a,b);
	insert into t1(a,b) values ('test','TEST'); 

So you will have an encrypted database with 
one table named "t1" of two columns which 
contains "test" and "TEST". How do we break it? 
Here's the shell (bash) script I used:

	max=10000; #FourDigitPin
	DATUM=$(date +%s);
	counter=0;

	echo $DATUM $counter >> logfile.txt
	
	while [ ${counter} -le $max ]; do
   		
		counter=$(($counter + 1));
	   		
		DATUM=$(date +%s);
   		
		echo "PRAGMA KEY="$counter";" > init.txt
   		# echo $DATUM $counter >> logfile.txt;

   		if `./sqlite3 -init init.txt test.db "select * from t1;" | 
		grep "test" 1>/dev/null 2>&1`

   		then
        		echo $DATUM $counter >> logfile.txt
        		break;
   		fi
	done


So plain, straight and simple. But what are the results?

A 4 digit numeric PIN takes 6.8 min.
A 8 digiti numeric PIN takes 73 days.

Thats not too bad for small pc (2 GHz, 2GB Ram). 
But what about using a painful alphanumeric password:

A 4 character PIN takes 27 days.
A 8 character PIN takes 2.754.150 years.

In conclusion - you should be fine using an 
alphanumeric pin with at least 6 characters.
