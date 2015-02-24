---
layout: post
title: How install MySQL on Mac OS X
categories: [MySQL]
tags: [MySQL, Mac OS X]
fullview: true
---

####Steps:

1. To download, click [here](http://dev.mysql.com/downloads/mysql/). (Recommend DMG Archive)
2. Double click the DMG Archive to install. Click "Continue"
3. System Preferences.. -> MySQL -> Start MySQL Server
4. Open Terminal and type 	

		$ /usr/local/mysql/bin/mysql -u root -p		

5. The default root password is blank.
6. Enjor your coding!



####Ps.

	Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
	
means you havn't started the MySQL Server. Do step 3.


	ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)

means the password you entered is wrong. See step 5.