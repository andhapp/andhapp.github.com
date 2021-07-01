---
layout: post
title: When Zeus doesn't work...
---

Do you work with Rails? and is it not a brand spanking new Rails 4, but the older and less-loved, relatively speaking, version?

Then, you must have come across Zeus. It's pretty handy if you like to test drive your code from outside-in and aren't scared to venture into the dark and a tad dragging land of integration specs. A usual Zeus workflow is, to start the server first, and then issue commands to the server from the client. Simple!

However, it's not always like it. You may come across unhelpful error messages, like the following when you start the server:


<code>
exit status 1 and then run tests.
</pre>

or

<code>
Could not find 'zeus' (&gt;= 0) among 214 total gem(s) (Gem::LoadError)
</code>

Both the error messages are very random. Googling the first one will reveal a lot of reasons and ways to fix it, the second one is just a usual gem error message when the gem is missing. In both the cases, I found the reason for the error to be some gems missing from project’s bundle and installing those gems fixes the issue.

So, next time when you pull upstream changes, and Zeus stops working, try running `bundler's install` command.

Hope it helps.
