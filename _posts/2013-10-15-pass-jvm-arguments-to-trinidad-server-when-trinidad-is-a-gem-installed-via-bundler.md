---
layout: post
title: Pass JVM arguments to Trinidad server when trinidad is a gem installed via
  Bundler
---

I've experienced some OutOfMemoryError on my JRuby app and all the googling has led me to one solution, that is, pass the -Xmx, -Xss, and -Xms options to JVM. Now, it's easy to do it with Java, or JRuby as you just pass it in, but I'm using [trinidad](<https://github.com/trinidad/trinidad>) and just run:

<pre>bundle exec rackup -s trinidad
</pre>

How do I pass any JVM options in this command?

A little bit of searching in trinidad's wiki, found a [performance tuning page](<https://github.com/trinidad/trinidad/wiki/Performance-Tuning>), which tells a way to do it but you have to run the app via jruby command, and not using bundle exec. I can't do that because my gem and other dependencies for it are managed by bundler. Well, here's a way to do that:

<pre>bundle exec jruby --server -J-Xmx2048m -J-Xms2048m -J-Xmn512m -J-XX:MaxPermSize=512m -S trinidad -e production
</pre>

Please note running it via bundle exec will slow down the startup, but it's okay. It's a one-time cost that I'm willing to pay for a huge win.

Hope it helps others.