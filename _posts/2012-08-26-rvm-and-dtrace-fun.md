---
layout: post
title: RVM and DTrace fun
---

The first think we learn as programmers is DRY i.e. Don't Repeat yourself yet we programmers break that principle all the time, sometimes unknowingly, and sometimes on purpose. Writing a gem is easy, but why write one from scratch when one can extend and improve an existing gem. Anyways, just my opinion.

I never understood the reason for [rbenv](<http://rbenv.org/>). I love [rvm](<http://rvm.io>) far too much to move to rbenv. My work colleague suggested that rbenv is much faster than rvm. I just ignored him then, but later on decided to investigate it further. I decided to write a small [Dtrace script](<https://github.com/andhapp/dtrace/blob/master/process_aggregation.d>).

It's a very trivial DTrace script. It collects and displays the process count called in the background. So, if it just lists the process (or scripts) with the count when I execute bash. In my bash script, I had the following line which loads rvm and allows for selecting gemsets and rubies.

```
if [[ -s ~/.rvm/scripts/rvm ]] ; then source ~/.rvm/scripts/rvm ; fi
```

Here are the results:

![RVM v Rbenv](/assets/rvm-v-rbenv.png)

In short, rvm script makes quite a few extra calls and that makes it different from rbenv. But, it's not a significant difference for me to switch or write another library that does exactly the same.

If you think about it, RVM is trying to solve two problems:

1. Store gems based on projects, so one can easily separate a Rails 2.3 application's gems from Rails 3's gems.

1. Easily switch between different rubies.

Does it need to do that? In my opinion, Bundler is quite good at managing gems. Therefore, my solution to this issue is to not create gemsets. That's exactly what rbenv does. In the meantime, I have created a simple bash function to load rvm shell on demand.
