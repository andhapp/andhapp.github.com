---
layout: post
title: Apache on Mac
---

To restart apache on Mac, all you need to do is uncheck(and check) Web Sharing through your System Preferences -> Internet and Network -> Sharing but what it does not tell you is any error messages in the config. Therefore, it would look like that the apache has restarted but the server would still not work. If that is the case, just run:

<pre>/usr/sbin/httpd
</pre>

in the Terminal and it will spit out any errors.