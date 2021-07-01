---
layout: post
title: 'Unix pipes don''t work with cd '
---

I use pbcopy (on mac) to copy the current working directory path:

<pre>pwd | pbcopy
</pre>

But, the following redirection doesn't work:

<pre>pbpaste | cd
</pre>

This command will just take me back to the my home directory. Why does this redirection not work?

Replacing cd with less works as normal, that is, the output of pbpaste is given to the next command as input:

<pre>pbpaste | less
</pre>

The reason cd doesn't work with redirection is because cd is not an external command. It's a shell builtin function and it runs in the context of the current shell, and not as an external commands, in a different process. The right way to use cd with pbpaste is to do this:

<pre>cd $(echo `pbpaste`)
</pre>

Hope it helps.

**Update (2014-10-20)** After recently reading Unix Shell in Ruby, I think the builtin commands can be explained much better with the following excerpt I took from the book:

*Every shell has some built in commands. These are commands which are inherently different from typical utilies in that they change the state of the shell and run in the shell process itself. For instance, a utility like cat simply prints text to the terminal. It does not change the state of the shell itself. The same goes for common commands like grep, tail, and curl. But there are certain commands that need to change the state of the shell, and cd is one of them.*