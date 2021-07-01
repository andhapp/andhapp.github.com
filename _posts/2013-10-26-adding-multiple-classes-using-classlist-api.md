---
layout: post
title: Adding multiple classes using classList API
---

This week, I ran into classList API, properly. I've read about it in the past, but never had the chance to use it. Most of the articles on google, just give you an introduction into classList API, but fail to reveal the full picture. For instance, I was trying to add multiple classes to an element in the DOM and kept getting errors. None of the articles could solve the mystery behind it.

I decided to do my own research and ended up on the [current DOM spec](<http://www.w3.org/TR/domcore/>).

classList API is a convenient way to access and manipulate the classes for an element in the DOM. In the background, it implements [DOMTokenlist interface](<http://www.w3.org/TR/domcore/#interface-domtokenlist>). The interface clears all the confusion and below is the code to add multiple classes:

<pre>document.getElementById("some-element-id").classList.add("class1", "class2");
</pre>

Can you spot any issues with the way the API works?

Well, it doesn't work like jQuery's (or zepto) API for adding classes. In popular javascript frameworks, you will do something like this:

<pre>$('#some-element-id').addClass("class1 class2");
</pre>

Does it have to work like jQuery? It doesn't have to work like any of the javascript frameworks out there, but I was expecting it would try and stay close to the existing trend. But, it doesn't. Anyways, I continue to live and learn.