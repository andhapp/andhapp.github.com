---
layout: post
title: Cygwin, RSpec on Windows Vista
---

I have turned into an early adopter for some reason, so few weeks back when I had the opportunity to use [Rspec ](<http://rspec.info/>)to do some [TDD](<http://en.wikipedia.org/wiki/Test-driven_development>) style of development...I literally jumped on the idea. But the adoption was not that easy or straight forward. Anything on [Windows](<http://www.microsoft.com/windows/windows-vista/default.aspx>) does not work the first time there is always some tweak one has to do in order to get things working.

Well, I started the terminal on my Windows machine and went to the project directory...and ran the autotest command. I am a great fan of autotest and I have been using it with [Snarl](<http://www.fullphat.net/index.php>)(windows equivalent of Mac's growl) for nice error/success messages. Right, so I did autotest and it gave me some weird errors...I started thinking about all the steps involved and could not think of anything obvious. Went straight to [Google](<http://www.google.co.uk/>) and found out that autotest looks for an environment variable HOME when it fires up and for some reason Windows defines the path to the user's home directory as HOMEPATH as opposed to just HOME. To be honest autotest should be intelligent enough to figure that one out as well. Anyways, I set the HOME environment on my windows machine to C:\Users\{my\_username} and everything works like a charm.

But hang on...just like in software you fix one thing and break something else the [Cygwin](<http://www.cygwin.com/>) installation just went haywire...and for some reason it did not pick up the default settings I had set earlier on. Since I did the Rspec changes few days before the cygwin incident I could not relate them at all. I was left frustrated and I knew it must be because I have changed something recently. Finally, I figured it out that setting a HOME environment variable basically overrides the one defined by Cygwin and since the new HOME environment is pointed at a different directory, Cygwin just stops working.

Well, autotest does not really care what the HOME is...it just needs a HOME environment variable to work. So, I changed the HOME to point to Cygwin's HOME and now everything works as it should. But it took me some hours of frustration and that really makes me unproductive. Sometimes I wonder why do I use Windows. Should not bother with all this and should buy a [Mac](<http://www.apple.com/uk/mac/>)...or may be move to [Ubuntu](<http://www.ubuntu.com/>).