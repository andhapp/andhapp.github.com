---
layout: post
title: Trunkly Chrome extension
---

[Yahoo](<http://www.yahoo.com>) announced quite a while ago that [delicious](<http://www.delicious.com/>) (their bookmarking tool) will be shut down and I started looking for alternatives. There are few things I am looking for in a bookmarking tool:

1\. I don't want to pay for it.<br>

 2\. It should have a nice interface to work with.<br>

 3\. It should have a browser extension for example: delicious Firefox extension was a pleasure to use.<br>

 4\. It should have a nice API to I can build my own extensions (provided none exists) or may be a desktop app.<br>

 5\. and I don't want to pay for it. :o)

Luckily, there is another similar bookmarking tool known as [Trunkly](<http://trunk.ly/>) which ticks most of my requirements except that I could not find a browser extension for the same. So, as I said, I scratched my own itch and built one for Chrome. One thing that must be said is that writing an extension for Chrome is the easiest thing I have done in a while. The documentation is amazing and if you can read the documentation and follow the samples then writing an extension will be a walk in the park.

At the moment, the code is very young and it uses HTML5 localStorage to save the API key which might [not be secure](<http://www.nczonline.net/blog/2010/04/13/towards-more-secure-client-side-data-storage/>) due to all sorts of reason but this is early days and I plan to change it in the later iterations or perhasp use the web database. The extension is not hosted in the Chrome store yet or anywhere else and if you do want to try it out just download the zip and load it in Chrome. The [code](<https://github.com/andhapp/trunkly-chrome>) is hosted on github and if anyone wants to improve it or hack it, please go ahead.