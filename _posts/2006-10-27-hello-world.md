---
layout: post
title: Tryst with WordPress
---

It took me a long time to install my local copy of wordpress.

Problem: For some reason the PHP install failed to recognise the existence of mysql on my machine and gave the following error "Your PHP installation appears to be missing the MySQL".<br>

 Environment: Apache 2.2 on Windows XP, PHP 5, MySQL 5<br>

 Solution: Make sure the extension=php\_mysql.dll is commented out in php.ini and that the extension dir variable in php.ini is amended from "./" to "C:/PHP/ext". Also please ensure the php\_mysql.dll is copied to system32 folder in windows and its location is explicitly added to the PATH environment variable. Then it should work straight away. I had few other trivial errors but I will let your ambitious self sort them out.