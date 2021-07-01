---
layout: post
title: Xcode shenanigans
---

Recently, I've been working on a Phonegap application and just wanted to share some Xcode gotchas.

1\. Xcode's crash reports are saved in **/Library/Logs/DiagnosticReports/**. This comes handy when Xcode crashes on you, sometimes. It doesn't happen often, but for instance you have an Xcode project open and you moved the directory where the project was with Xcode open all that time, it will crash. Just be aware.

2\. Xcode saves all the user project settings in another place. This is in **\~/Library/Developer/Xcode/DerivedData** directory. If you don't want Xcode to remember any of your settings (like what windows were open in the project for next time), or you just want to clear the project settings cache, just delete this directory and you'll be good as gold.

3\. Finally, Xcode is very clever like any other IDE out there. It remembers the projects you've opened recently and keeps a reference to them. Now, if you've moved a directory with Xcode still open, it may crash. Launching Xcode post crashing will just result in it crashing again, because it's trying to be clever, as expected, and trying to open the projects you had open before it crashed the last time. It's just like **stack too deep bug** that we are familiar with.

Xcode is a nice IDE for what it does, but sometimes if you stray from the golden path you can end up in a back alley not knowing where to turn to and by the way, these are three stack overflow answers in one post.