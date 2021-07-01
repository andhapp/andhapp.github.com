---
layout: post
title: IRB on roids
---

Any ruby developer knows about the interactive ruby shell or in short irb and I am quite sure they use it everyday for quickly testing little scripts out. And Rails offers its own console which is basically irb with rails framework loaded with a valid database connection for performing quick tests. Now, in order to make it easy on your eyes one can change the default output of activerecords in console. But the question remains how? Well, I found a gem called [hirb](<http://tagaholic.me/2009/03/13/hirb-irb-on-the-good-stuff.html>) which simply does that for you. It is quite easy to install and configure and it improves the overall formatting by leaps and bounds.