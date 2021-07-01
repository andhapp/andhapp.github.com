---
layout: post
title: RubyGems error on Windows
---

Recently, I wrote a [ubiquity](http://labs.mozilla.com/2008/08/introducing-ubiquity/) command called [epoxy](http://epoxy.andhapp.com/) which allows one to simply convert the code snippet in the browser to a url. It uses [OpenPastebin](http://www.openpaste.org/en/) API and I wrote a simple Rails App for making requests to the OpenPastebin web service.

The rails app itself was quite simple to do apart from one major issue - [RubyGems](<http://www.rubygems.org/read/chapter/3>). Well RubyGems itself was not an issue but since the vesion of Rails `2.2.2` on my Windows machine needed RubyGems `1.3.1` to work I decided to upgrade it. RubyGems is mainly used for installing new gems and I really like this plugin architecture where one can install any new gem and try it out with no incoveinence. So I entered the following command to update gems:

```
gem update
```

There were no error messages so I assumed it had all worked fine. So, I went back to the command line and entered to check if the version was 1.3.1 and there was an error message.

I tried reinstalling ruby and rubygems several times. Tried googling but did not really get anywhere with it. The big problem with this was I could not install new gems easily which kind of defeats the whole purpose of having rubygems in the first place. I kept trying for quite some time and then for no apparent reason I uninstalled ruby from the Program Files folder(where I usually installed it) and installed it in `C:` instead.

Updated gems and this time it did not give me any errors. I did it as a test just to see if it works and it does. It is quite strange and I would like to look into the RubyGems update script to see if there is anything in there resulting in the error but have not had time to do it yet. This was one of those issues which was not really stopping me from working but I always had it at the back of my mind and am more than pleased to have resolved it.
