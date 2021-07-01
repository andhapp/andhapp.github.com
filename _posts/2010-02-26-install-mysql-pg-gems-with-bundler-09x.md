---
layout: post
title: Install mysql, pg gems with bundler 0.9.x
---

If you use ruby on rails, at some point you have to install mysql and pg gems (no offences to sqlite) and for some reason I keep forgetting the whole install procedure. Silly me! This post is dedicated to the loss of build\_options.yml in bundler 0.9.x and my subsequent struggle and frustration to install mysql and pg gems and the occurence of eureka moment proving why I am still a n00b.

Let us cut to the chase. [Bundler](<http://github.com/carlhuda/bundler/>) is the new gem dependency superhero. If you didn't know it perhaps you need to wake up and start using that thing they call the feed reader and subscribe to some ruby and rails feeds. The fun of working with open source is that one day you wake up do a git pull and everything stops working. It is quite like your life, everything is going swimmingly and then the most unexpected thing hits you.

Bundler 0.9.x leaves no stone unturned in frustrating you, if you had accustomed to the comfortable 0.8 api. However, after a a while you do realise the benefits of the changes. In 0.8 there was a way to specify build\_options (via build\_options.yml) to install gems like mysql and pg. That has disappeared in 0.9. I added an [issue](<http://github.com/carlhuda/bundler/issues/issue/23>) and you can see how it has taken shape in last few weeks. But what now? I can't run rails test on my machine now. I was so looking forward to refactor the hell out of active-record's relation class. I spent quite sometime wondering how the hell can I install mysql and pg gems using bundler.

It is quite simple if you think about it. mysql and pg gems need to know the location of mysql and pg on your machine. It should have been added to the PATH when they are installed but for some reason it did not. So, what you gotta do is simple. Add them to the PATH so when bundler installs them it can resolve the dependencies. Here are the commands:

<pre>export PATH=/usr/local/pgsql/bin:${PATH}
export PATH=/usr/local/mysql/bin:${PATH}
</pre>

And then just run bundler's install command. Voila!

I am so glad to have figured this out as now I can go back hacking into rails.