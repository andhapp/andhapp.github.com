---
layout: post
title: Speed up tests in Rails
---

Testing has always been part of the Rails framework, right from the beginning. The whole TDD concept became hugely popular after Rails was adopted in the mainstream. It has been around but Web applications were tested in a different manner 10 years ago. On my first day as a Java Developer, I was told by a Senior Developer that you can't really test a Java web app by writing unit tests. I took his advice and frankly speaking, I didn't know better.

Anyways, I am not here to talk about my career. I have been doing Rails for quite a while now and on one project, test suite took about 30 minutes to run. I know, 30 minutes. Because, we didn't fake the calls to external APIs. How silly was that? So, recently I started working on the project and every time I ran the test suite, it took 2 minutes for them to run. That kind of put me off the whole testing thing. I mean what's the point. I can just write the code and use the good old presentation driven development, where if it works it works. If it doesn't, then we'll fix it. This strategy kind of works, but becomes a nightmare when one bug fix results in another regression bug.

I ventured out looking for solutions and I found that instead of fixing the issues around testing, community has moved to the whole client/server architecture towards testing. I started on Spork. It's a very nice idea but I don't want to muck about with my configs and do the setting up. The downside is that now I have to get the entire team to use Spork and set it up and all. I know it works and a lot of developers use it but I don't want to do it. Then, accidentally, I found spin. [Spin](<http://jstorimer.github.com/spin/>) is the same client/server idea but instead of a drb server, like Spork, it uses UNIX sockets for communication. There is absolutely no setup required. I have been using it on two different projects and it has worked nicely.

Some other solutions are to load your database in memory, easy to do with sqlite but with postgres you have to create a ram disk and load the database from there. Stop abusing machinist, factory\_girl and the like as they make db calls. Instead, use mocks and stubs.

But, I still think these are just workarounds for the existing problem with Rails load times and testing. Is there a better solution to this problem? How can I make my application testable, follow TDD and yet never have to worry about loading rails? I guess I need to objectify my application. I will probably talk about it in my next post.