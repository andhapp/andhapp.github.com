---
layout: post
title: Convert SVG to PNG on Mac OS X
---

Android’s WebView is very primitive in terms of rendering SVG images as the background. I decided to convert them into PNGs and test their rendering. I don’t have photoshop, and I could have used ImageMagick to convert SVGs to PNGs, but whilst googling I found another nifty utility to achieve the same, **qlmanage**.

In Mac OS X, [Quick Look](<http://en.wikipedia.org/wiki/Quick_Look>) allows one to quickly preview files. qlmanage is a tool used by Quick Look internally to generate the images for the preview.

Please note that it may be limited with how much it can achieve and is not comparable to something like ImageMagick, but still nifty when you don't have anything else installed on your machine.

Hope it helps.
