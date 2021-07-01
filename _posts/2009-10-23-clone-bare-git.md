---
layout: post
title: Clone bare git
---

Found an interesting option to clone a git repository. Honestly, speaking I have no idea how it could be usefult because it does not actually do a checkout of the HEAD. Anyways, if you run:

<pre>git clone --bare git://github.com/andhapp/decoct.git
</pre>

then you will have the following directory structure which is quite similar to what's in your project's .git folder.

<pre>-- decoct.git 
   -- HEAD
   -- config
   -- description
   -- hooks
   -- info
   -- objects
   -- packed-refs
   -- refs
</pre>

This is what the doc has to say:<br>

 \--bare : Make a bare GIT repository. That is, instead of creating <directory> and placing the administrative files in <directory>/.git, make the <directory> itself the $GIT_DIR. This obviously implies the -n because there is nowhere to check out the working tree. Also the branch heads at the remote are copied directly to corresponding local branch heads, without mapping them to refs/remotes/origin/. When this option is used, neither remote-tracking branches nor the related configuration variables are created.</directory></directory></directory>

This is exacly what it does but how would this be useful puzzles me.