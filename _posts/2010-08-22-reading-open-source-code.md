---
layout: post
title: Reading Open Source Code
---

I was very confused the first time I heard this phrase - "Read Open source code". I could not really grasp the concept of reading someone else's code. How can that improve your own programming skills? But, I can safely say that it does help. Two things that I found out recently, both reading some open source code. Here they are:

1\. I found this trick used in Paperclip's code. **rescue** is basically to catch the exceptions and do the needful but one can use them inline. Let us look at an example:

<pre># Usual Way
begin
  1/0
rescue =&gt; e
  puts "Exception"
end

# Cool way
1/0 rescue "exception"
</pre>

We all know what the first approach does. The second one is quite simple as well. Execute the code followed by rescue if there is an exception in the code before rescue. Now, I will agree that both approach has it merits but still the second one is much cooler and neater.

2\. Passenger is an amazing, cutting-edge library that I usually read through and there is something very interesting I found in the [code](<http://github.com/FooBarWidget/passenger/blob/master/lib/phusion_passenger/utils.rb#L426>). There is a library in ruby called [Etc](<http://ruby-doc.org/stdlib/libdoc/etc/rdoc/index.html>) that allows one to query stuff like the current user and so on. I had no idea one could do it.

Well, every programmer should read other's code and his own code from time to time to see what he could improve and where we went wrong.