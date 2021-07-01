---
layout: post
title: Comment multiple lines in MacVim
---

Commenting multiple lines is mostly used when one is debugging and quickly wants to take a piece of code out, just to put it back again. Here's how one can achieve in the same in MacVim.

1\. Press 'V' on your keyboard and use the arrow key to select the code snippet to be commented out.<br>

 2\. Then press ':' which will automatically change that to something like this:

<pre>:'&lt;,'&gt;
</pre>

3\. Then just type in this command and press Enter.

<pre>:'&lt;,'&gt;s/^/#/g
</pre>

Now, to uncomment them just follow steps 1 and 2 and then enter the following command:

<pre>:'&lt;,'&gt;s/^#//g
</pre>