---
layout: post
title: Moving from Dreamhost to Linode
---

Yes, after 3 years with DreamHost, I have finally moved my [blog](<http://www.andhapp.com/blog>) to a Linode server and it did not go as planned therefore, lack of activity on the blog. I never had any issues with it. It was cheap, gave me easy options to install WordPress and all. But being a programmer, I wanted to get the Server Admin experience under my belt and hence the move to a Linode server. I bought it quite a while ago but since I was in the middle of the DreamHost contract (bought a 3 year one), I left it running on it. Unlike my experience, several bloggers and developers had [issues](<http://www.cubiclecage.com/dreamhost-review-do-not-be-scammed-by-dreamhost/>) with DreamHost. You can [read](<http://www.upstartblogger.com/why-dreamhost-sucks>) about it [here](<http://blog.websitesbybarrett.com/past/2008/4/2/dreamhost_issues/>) and [here](<http://www.webhostingreviews.com/find-host.htm?text=dreamhost>). Let us be honest that it's good value for money.

It's not until you have actually moved that you realise the advantages of a hosting service. Things like mail server, I tried postfix and had numerous issues. But, thanks to Google apps [standard edition](<http://www.google.com/apps/intl/en/group/index.html>). E-mail works like a charm now. Setting up php with nginx and fast-cgi required a few hours and if you are not a developer or don't have the ambition to learn these things, DreamHost is your saviour.

If you ever decide to move from DreamHost to Linode, please note that DreamHost offers 60 days grace period for you to pay your bill or move your sites. I did not know it and had to move all the sites in a rush where I could have planned it and since DreamHost does not offer a static IP once you change domain's nameservers, you can't even access the MySQL database.

Also, remember one thing, no matter what never install a CentOS linux distro on your Linode. Tell you why in my next post.