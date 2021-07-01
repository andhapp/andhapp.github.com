---
layout: post
title: 'Rails Input output error on linux '
---

If you are getting input/output error on linux rendering .rhtml pages then the only way you can resolve it is by freezing the version of rails...just do:

rake rails:freeze:gems

This command will freeze this rails application to the version of Rails on the server. If you want to delve deep click the link : [Freeze Rails](<http://support.tigertech.net/freeze-rails>)