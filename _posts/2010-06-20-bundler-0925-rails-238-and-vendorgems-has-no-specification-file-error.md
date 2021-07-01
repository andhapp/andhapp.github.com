---
layout: post
title: Bundler 0.9.25, Rails 2.3.8 and vendor/gems has no specification file error
---

Majority of us have seen this dreadful error after running rake:gems:unpack or a similar command to register gems with the application.

<pre>config.gem: Unpacked gem clearance-0.8.8 in vendor/gems has no specification file. Run 'rake gems:refresh_specs' to fix this.
</pre>

I was under the impression that this happens due to some bug in rails gem dependency management and never expected the same to happen with [Bundler](<http://github.com/carlhuda/bundler>). Unfortunately, I was wrong. Just yesterday, I had this error and it's one of those things that doesn't really stop your app from working but is very annoying.

There is a [fix](<http://stackoverflow.com/questions/625464/rake-gemsrefresh-specs-error-on-unpacked-gems>) on Stack Overflow but it might not work if you are using bundler. The command to use remains the same but it needs to be slightly modified. Here are the steps:

This assumes that you get this error with clearance.<br>

 Step 1

<pre>cd vendor/gems/clearance-0.8.8
</pre>

Step 2

<pre>gem specification ../../cache/clearance-0.8.8.gem &gt; .specification
</pre>

With bundler the gem files are actually stored in the vendor/cache directory. specification is a gem command that extracts a .specification file from gem file. [Here's](<http://docs.rubygems.org/read/chapter/10#page37>) full explanation of it.

That's it. Wasn't that easy?