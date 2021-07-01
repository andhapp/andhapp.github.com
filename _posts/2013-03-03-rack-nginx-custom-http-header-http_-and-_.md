---
layout: post
title: Rack, Nginx, Custom HTTP header, HTTP_ and _
---

A while back, I was working with an application that used custom headers. Applications use custom HTTP header to transfer domain specific information, either in request or response. Earlier the trend was to prepend "X-" to the custom header, but since [June 2012, this approach has been deprecated.](<http://tools.ietf.org/html/rfc6648>)

I used rack-test to write some tests and to my surprise it appends HTTP\_ in front of custom headers. I think it may do that in front of other headers too, and I did read this somewhere, but I can't seem to find that link anymore. So, the first lesson of this post is to make others aware that HTTP\_ is appended to custom headers with rack.

All this worked smoothly in local environment, and the moment I pushed it to Nginx+Passenger, it just blew up. Debugging revealed that it was actually just the way custom headers are treated in Nginx. The custom header had underscores in it, and [Nginx is known to ignore custom headers with underscores](<http://nginx.org/en/docs/http/ngx_http_core_module.html#underscores_in_headers>), and therefore, this custom header never made it to the actual application. For example: X\_API\_KEY will be ignored by Nginx, where as X-API-KEY will be translated into X\_API\_KEY. I had to change the custom header to X-API-KEY and remove the underscores.

To summarise, these are the stages a custom header goes through:

1\. Starts it's life as X-API-KEY in the client request

2\. Reaches Nginx, and is changed from X-API-KEY to X\_API\_KEY

3\. Reaches Rack, and is changed from X\_API\_KEY to HTTP\_X\_API\_KEY

4\. Should be interpreted as HTTP\_X\_API\_KEY in the actual application code.

Hope it helps anyone facing a similar issue.