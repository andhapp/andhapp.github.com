---
layout: post
title: Moving this blog from Dreamhost to Linode
---

This post is in continuation to my earlier [post](<http://www.andhapp.com/blog/2010/11/07/moving-from-dreamhost-to-linode/>) which simply mentions the move of this blog from Dreamhost to Linode and this post is an attempt to expound on a little bit of the details and the experience.

This was not just a move from shared hosting a.k.a Dreamhost to a vps solution a.k.a Linode, but it was also a move from Apache to Nginx + fastcgi. Yes, now I am actually running the Wordpress blog on Nginx. It's just a matter of choice really. There is nothing wrong with Apache. It's just that I have been using Nginx with Passenger for Rails deployment and decided to keep everything under one hood.

### Say NO to CentOS

If you are like me (not very bright), you will instantly google "setting up nginx with fastcgi" and like always google will not disappoint you. But this information overload becomes a pain in the back side, sometimes. Why? Well, if something worked for someone does not mean it will work for you and then how long ago was it and has something changed since then and so on and so forth. CentOS has outdated packages and in several cases broken. Also, most of the results you found whilst googling suggest creating a startup script for php with fastcgi and refers to the use of start-stop-daemon and CentOS does not have one. Therefore, to keep it simple just go with ubuntu. Trust me. However, if you insist on installing CentOS then [here](<http://centos.org/modules/newbb/viewtopic.php?topic_id=24207&forum=40>) are few [workarounds](<http://florent.clairambault.fr/get-start-stop-daemon-on-any-linux>) for the start-stop-daemon problem.

### Install dependencies manually

What exactly do you need to run this blog? PHP, MySql, and Nginx along with fastcgi and the most important, configure Nginx to proxy all the .php requests via the fastcgi server. Here's a [link](<http://tomasz.sterna.tv/2009/04/php-fastcgi-with-nginx-on-ubuntu/>) that I found extremely helpful in installing all the above mentioned softwares. However, my nginx.config is slightly different from the one mentioned in the link. Here's how mine looks:

```
server {
  listen 80;
  server_name <server_name>;
  root <document_root>;
  index index.php index.html;
  location ~ \.php$ {
    include <location_of_fastcgi_config file="">;
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_index index.php;
    keepalive_timeout 0;
  }
}
```

Replace the values in "<...>" with your own specific values.

I create a new `fastcgi_config` file for each domain and the only value I change is the document root. 

Here's an example:

```
fastcgi_param GATEWAY_INTERFACE CGI/1.1;
fastcgi_param SERVER_SOFTWARE nginx;
fastcgi_param QUERY_STRING $query_string;
fastcgi_param REQUEST_METHOD $request_method;
fastcgi_param CONTENT_TYPE $content_type;
fastcgi_param CONTENT_LENGTH $content_length;
fastcgi_param SCRIPT_FILENAME <document_root>$fastcgi_script_name;
fastcgi_param SCRIPT_NAME $fastcgi_script_name;
fastcgi_param REQUEST_URI $request_uri;
fastcgi_param DOCUMENT_URI $document_uri;
fastcgi_param DOCUMENT_ROOT <document_root>
fastcgi_param SERVER_PROTOCOL $server_protocol;
fastcgi_param REMOTE_ADDR $remote_addr;
fastcgi_param REMOTE_PORT $remote_port;
fastcgi_param SERVER_ADDR $server_addr;
fastcgi_param SERVER_PORT $server_port;
fastcgi_param SERVER_NAME $server_name;
```

You can read [here](http://wiki.nginx.org/NginxFcgiExample) for more information on the nginx fastcgi. Creating a new config file for each domain is just stupid and you can just pass the values of dynamic variables like `DOCUMENT_ROOT` or `SCRIPT_FILENAME` from within nginx but I could not get it to work.

### Install dependencies via Chef

I think installing everything manually is a bit backward and one could always use <a href="http://wiki.opscode.com/display/chef/Home">Chef</a>. In my next post, I will talk about my experience of setting up an entire server using Chef. Chef's wiki is amazing and takes you through each and every step. Give it a try.

### Gotchas

* Make sure you restart `fastcgi_server` as I totally forgot and it never picked up mysql.
* Also, add `mysql.so` and `mysqli.so` to your `php.ini` file and restart `php_fastcgi` server for it to pick up the changes. It's most probably in `/etc/php5/cgi` directory.

It took me quite sometime to really get everything working and I was tempted to just give up and just use apache. But I stood my ground and finally cracked it. I hope it helps you in your own endeavours.
