---
layout: post
title: Firefox 3 tweak
---

I finally figured out how to do this. Well I wanted to open the search results in a new tab whenever I searched for anything using the Google search box (next to the address bar). I thought that it was part of some add-on I had before but I could not remember it. Eventually, I started looking into the Firefox config and found that a little tweak alters the behaviour of Firefox.

Right, so what you have to do is type "about:config" in the Firefox address bar and it will display a list of all the Firefox configurations. Actually it should show you a warning message just say yes to it. Now what you have to do is filter for "browser.search.openintab" in the filter box. So just type this in or copy paste from here. It would filter as you type so once you have finished typing the whole thing it will just display this option. Double click on it to set it to true and restart your browser. Now go and search for something and you do not have to open a new tab for it. It will display the serch results in a new tab. I wonder why was this option not set to true by default.

I am pleased that I figured this one out.