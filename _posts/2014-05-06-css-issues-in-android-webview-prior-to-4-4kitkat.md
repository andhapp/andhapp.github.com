---
layout: post
title: CSS issues in Android WebView prior to 4.4(kitkat)
---

Should you venture into developing a hybrid app for Android WebView in versions before 4.4?

NO. Unless you liked fixing bugs for IE6 when you knew that IE8 or IE9 were a bit better and people should just upgrade their browsers. Although, upgrading OS on devices running Android is quite complicated, and should be dealt in a separate post.

With 4.4, the WebView uses Chromium rendering engine, which is most up-to-date and implements the HTML, CSS, and JS specs correctly. Anything before that used a native Android rendering engine which was buggy and didn't implement the spec properly. Now, the 'business' won't like you distancing yourself from the older versions because as it happens, a lot of users are still running the older version, for example, 4.3, and 4.2.2.

What can you do in such a scenario?

There's not much you can do, really. Bite the bullet and fix them bugs. With hybrid apps, you can use Android specific stylesheets (in Cordova) to workaround the problems. Android forums aren't of much help because they simply refuse to backport any bug fixes made in 4.4 (since the whole WebView implementation has been re-written), and your best resource is StackOverflow.

Device (hardware), OS, and screen size for Android can result in endless permutations, and making a choice of supported devices and getting things to look and work consistent across all the possible combination is crazy. It's like browser wars amplified.