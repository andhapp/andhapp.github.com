---
layout: post
title: Moving to gVim slowly and steadily
---

I recently (2-3 weeks ago) just decided to move to [gVim](http://www.vim.org/download.php). No apparent reason except the fact that I have been doing quite a bit of linux server managerment and have been using the default vi editor so why not use it all the time. I had no idea of the challenges but I guess that makes it more fun when one overcomes the small challenges and celebrates the little achievements.

The first and foremost thing about any editor is the way it looks. It "should" be presentable and pleasing to the eye. I started looking into the [plugins ](<http://www.vim.org/scripts/index.php>)and found one called BusyBee. Installed it and it seemed to work (no offences to the creator) but it was not that great. To be honest theme for your text editor is more like a taste thing everyone's bound to be different. I kept looking and googled for Textmate themes for Vim and found some brilliant ones. The one that I am using now is [ir\_black](<http://blog.infinitered.com/entries/show/8>). To make sure this scheme is used as a default, I added the following to my \_vimrc file:

In addition to the theme, I am using the following plugins at the moment:

* [rails](http://www.vim.org/scripts/script.php?script_id=1567) - amazing plugin for rails development with vim. Found an amazing [tutorial](http://biodegradablegeek.com/2007/12/using-vim-as-a-complete-ruby-on-rails-ide/) to set it all up. The same tutorial also delves into several other plugins.</li>

* [matchit](http://www.vim.org/scripts/script.php?script_id=39")

* [repeat](http://www.vim.org/scripts/script.php?script_id=2136)

* [surround](http://www.vim.org/scripts/script.php?script_id=1697)

* [project](http://www.vim.org/scripts/script.php?script_id=69)

* [dbext](http://www.vim.org/scripts/script.php?script_id=356)

I am still learning the tons of commands in these plugins but on a positive note getting better day by day. At the moment I have turned off the option to backup the files otherwise it creates the `\~filename.rb` like files and I do not want to do that as I check everything into my [git repository](http://github.com/andhapp/).

One more thing, after every edit you must come out of the `insert mode` and do `:w!` to save the changes. I cannot be asked to do that everytime I do edits. It was just getting painful so I added the following mapping to my `_vimrc` file:

```
map ⟨Esc⟩ :w!⟨CR⟩
```

This maps my `Esc` key (which I press anyways to come out of the insert mode) to trigger `:w!<cr>`(CR bascially means Enter). I was expecting that this would basically just save the file when I hit Esc. However, it does not work as expected. So, when I hit Esc the first time it will exit the `insert` mode but not trigger this command. But on hitting Esc again it does save the changes. So, my next task is to find out the current mode and if it is `insert` do two Esc and then save the file otherwise do as above.</cr>
