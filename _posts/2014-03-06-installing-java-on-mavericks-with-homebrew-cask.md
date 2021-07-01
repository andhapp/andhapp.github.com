---
layout: post
title: Installing Java on Mavericks with homebrew-cask
---

Years ago, when I used to develop on a Windows machine, a senior colleague of mine told me - "Apple's version of Java is slightly behind". Ofcourse, I was oblivious to the control tech giants can force on it's users. Anyways, whilst setting up my machine for some Android development, I had to install Java. I had JRE installed to run applets (who does that now?) in the browser, but for android development you need JDK.

While googling, I stumbled upon [homebrew-cask](<https://github.com/phinze/homebrew-cask>) and I was totally blown away. You can literally download the binaries and have them install by just running one command on the Terminal.

<pre>brew cask install virtualbox
</pre>

Shut up and take my money!

I ran commands for VirtualBox and Genymotion and it worked like a charm. However, when it came to installing Java, it fell flat on it's face. Homebrew-cask downloaded the java binary to this directory:

<pre>/opt/homebrew-cask/Caskroom/
</pre>

but just left it there. I was still stuck on 'no Java' issue, so I just double-clicked the binary to install it. It installed properly and I was on my way to some andorid enlightenment, but the process revealed two things that need more investigation:

1\. homebrew-cask has a bug somewhere as it failed to install Java binary.

2\. Now, it's easier to just run one command and install Java. I always find it really challenging to find the right binary on Apple's site to install.

Hope it helps anyone needing Java, and unknown to homebrew-cask.