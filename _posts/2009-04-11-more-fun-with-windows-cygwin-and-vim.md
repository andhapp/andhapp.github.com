---
layout: post
title: More fun with Windows, Cygwin and Vim
---

Developing on a windows machine has guranteeed me loads of fun in last few months. Anyone can tell that by looking at my last few posts. My aim is to keep working on Windows as long as I can without losing my patience and I have managed to do that quite well for so long.

I [have been working](<http://www.andhapp.com/blog/2009/03/14/moving-to-gvim-slowly-and-steadily/>) with Vim for quite some time now. Recently, I was told about a [brilliant tutorial](<http://www.akitaonrails.com/2009/01/04/rails-on-vim-in-english>) on using Vim for Rails and other plugins. Well, I forked the [project](<http://github.com/andhapp/vimfiles/tree/master>) and downloaded the vimfiles and added them to my installation. I could have followed the steps specified by Akita on using the plugins on Windows but then again where is the fun in that...and I want to learn these things by doing it.

Well I was really looking forward to the [fuzzy\_finder\_textmate plugin](<http://github.com/jamis/fuzzyfinder_textmate/tree/master>) where you can map the any key to open up the finder (equivalent to Mac Textmate finder). But it did not work. Instead it gave me an error that it could not find the fuzzy\_file\_finder.rb file. This is a ruby file which enhances the original fuzzy\_finder plugin. After some digging around, I found that for some reason it was using:

<div style="padding: 15px; background-color: rgb(224, 224, 224); color: black;"><code>require "#{ENV['HOME']}/.vim/ruby/fuzzy_file_finder"</code></div>

Since, I am using cygwin my HOME variable is pointed to my cygwin home directory which does not have a .vim folder. Also, on Windows Vim is installed in the Program Files where all the plugins and other vim files are and that is where this ruby file was. I changed the path to use the ruby file and it started working. I am pleased that it was resolved in the end but can it get extremely painful at times. Do check out akita's video on setting up Vim for Rails.