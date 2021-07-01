---
layout: post
title: Sayo nara hideous urls
---

I have managed to get rewrite urls to work for this blog. It was not difficult at all but I was just being lazy (not a GTD attitude I know)...so no more of `index.php?p=12` in the url instead you will be presented with a pretty url for example `sayo_nara_hideous_urls/14` (more meaningful and is same as the post title). It was not that difficult...tweaking the php code a little bit and adding few rewrite url rules (regular expressions rocks) in `.htaccess` will do the trick.

Nevertheless, there are few things that still needs to be fixed:

1. What if I use characters like `?` or `...` in my post title or categories? I think then it will just fall over so I need robust rules to handle that situation.

1. I could not get the search function to show up in a pretty url way...but these two are my next actions.
