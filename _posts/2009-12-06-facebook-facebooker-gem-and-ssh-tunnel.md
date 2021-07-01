---
layout: post
title: Facebook, Facebooker gem and ssh-tunnel
---

Well, it was long hours of endless frustration and little fun, I tell you. That is how I spent most of my saturday trying to follow the instructions to create a ssh-tunnel so that I could test facebook application as I developed it. Putting an application up on facebook is a walk in the park. You create a new application, give it a callback url, where it can find what to display in your application and you are done. As far as your callback url is legitimate your application will work like a charm. If you are interested, please go ahead and check the request-response [artchitecture](<http://wiki.developers.facebook.com/index.php/Random_questions#Basic_Application_Architecture>).

I am using the facebooker gem which gives a you a lot of functionality out of the box and one thing it does is gives you rake tasks to start a ssh-tunnel. The purpose of ssh-tunnel is simple port-forwarding. So, any requests to a publicaly available domain at a certain port should be forwarded to the local server where I am doing facebook application development. The latest version of the gem sits on github and you can install it as a plugin, just do:

<pre>script/plugin install git://github.com/mmangino/facebooker.git
</pre>

There are [several](<http://apps.facebook.com/facebooker_tutorial/>) [tutorials](<http://www.ajaxlines.com/ajax/stuff/article/getting_started_with_facebooker.php>) that describe how you can set it up, just google it.

And I will go straight into the ssh-tunnel part of the problem so I assume that you have facebooker gem installed and you have made necessary changes to the facebooker.yml file by adding your public host name and ports where you want to achieve port forwarding. For example: any publicly available domain that you have ssh access to can be used as a port-forwarder. For the sake of this post let us say:

<pre>public_host :andhapp.com
remote_port: 4007
username :andhapp
localhost :localhost
local_port :3000
</pre>

As per the above details, when I run the facebooker rake task to start the tunnel I will basically be doing this: Any requests to andhapp.com on port 4007 should be forwarded to my localhost on port 3000 (which is where your dev facebook app is running).

Once it is all set-up you can use facebooker's nifty rake command to start the tunnel, like this:

<pre>rake facebooker:tunnel:start
</pre>

This would prompt you for your password for sshing to your public host. To check the ssh-tunnel status, just do:

<pre>rake facebooker:tunnel:status
</pre>

If this command comes back with "Seems, ok" you know the ssh-tunnel is up and fine. But when you access http://andhapp.com:4007 (or whatever domain you have used) it just gives you a browser error - "the connection could not be made". It took me a long time to figure out what exactly the problem is. The ssh-tunnel is fine its the way ssh is configured. To fix the issue, just uncomment the line:

<pre>GatewayPorts no
</pre>

in your ssh config file on your server, most probably found in: /etc/ssh/sshd\_config and change it to:

<pre>GatewayPorts yes
</pre>

Restart ssh, and restart the tunnel and it will start working. What the hell? Why do we need to do that for? Here's an [explanation](<http://www.snailbook.com/faq/gatewayports.auto.html>).