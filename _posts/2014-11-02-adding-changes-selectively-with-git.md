---
layout: post
title: Adding changes selectively with Git
---

Here's a scenario for you developers:

1. You are happily hacking on a feature from the beach.

2. But, someone on your team is waiting for your changes to go in because they need a few methods on a class you will add as part of your changes.

3. You have written those methods but the whole functionality still needs work so you can't commit it in.

4. You don't want the other members of your team to wait.

5. They could work from your branch, but that would mean their work will now wait for your work to go in first.

6. Or you could selectively add a couple of methods you have written in the class for them to use.

7. But, is there a way to selectively add and commit files in git?

Yes, you can with git's interactively adding a file feature. Below is a better explanation of the same feature with a little scenario:

Imagine I have a git repository with one file called `first.txt`. The file's contents in the remote repository are:

```
code-for-blog(master)$ cat first.txt
This is first bit of text.

This is second bit of text.

This is third bit of text.
```

I am working through this file and update the contents to something like:

```
code-for-blog(master)$ cat first.txt
This is first bit of text.

This is second bit of text.

This is third bit of text.

This is fourth bit of text.

This is fifth bit of text.

This is sixth bit of text.

This is seventh bit of text.

This is eighth bit of text.
```

Now, I only want to commit the last 2-3 lines of this code. I have two options, either, I cut all except last 3 lines that I've added since the last commit and check it in and then paste the lines I cut, back into this file. That could work, but, imagine if you have to do the same across 3-4 files. Not very efficient, is it?

Or you could use the interactive tag for the git's `add` command. We will take the same file (I've been talking about) as an example and try to add and commit only the last 3 lines of this file.

On running the following in a working directory

```
git add -i
```

you will see a menu with a list of files and commands one can run on the file.

```
code-for-blog(master)$ git add -i
           staged     unstaged path
  1:    unchanged       +10/-0 first.txt

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
```

We would like to add only some selected lines we need to enter `p`(which stands for patch). This will drop you into a `patch` submenu like the one below. In the patch submenu, you will be able to select the file that you would like to patch. In this case, the letter `f` is the cue for it. Entering 'f' on this submenu and returning will show the same menu again, but this time, you will see that there's a `\*` next to the file number on the left. In this case, `1` became `\*1`.

```
What now> p
           staged     unstaged path
  1:    unchanged       +10/-0 first.txt
Patch update>> f
           staged     unstaged path
* 1:    unchanged       +10/-0 first.txt
Patch update>>
```

After the file selection has been made, pressing enter at patch update prompt will drop you into the file, like the screenshot below. You can see the lines that have been added since the last commit. At the bottom, you can see a set of commands that can be run at this stage. You can see the explanation of these commands by typing `?` and pressing enter.

```
Patch update>> f
           staged     unstaged path
* 1:    unchanged       +10/-0 first.txt
Patch update>>
diff --git a/first.txt b/first.txt
index fa9e9e5..e2581bc 100644
--- a/first.txt
+++ b/first.txt
@@ -3,3 +3,13 @@ This is first bit of text.
 This is second bit of text.

 This is third bit of text.
+
+This is fourth bit of text.
+
+This is fifth bit of text.
+
+This is sixth bit of text.
+
+This is seventh bit of text.
+
+This is eighth bit of text.
(1/1) Stage this hunk [y,n,q,a,d,e,?]?
```

I want to add the last 3 lines, I type `e` and press enter. `e` stands for manual editing. This will open up the same file in your default editor. Usually, that's determined by `$EDITOR` environment variable.

After editing and saving the file, I will be returned to the first menu again. Type `s` and press enter to check the status of the files in the working directory. The status shows that 3 lines have been staged and there are still 7 unstaged lines remaining for file `first.txt` which is what we set out to achieve.

```
What now> s
           staged     unstaged path
  1:        +4/-0        +6/-0 first.txt

*** Commands ***
  1: status	  2: update	  3: revert	  4: add untracked
  5: patch	  6: diff	  7: quit	  8: help
What now>
```

There are a lot of other commands in the menu that shows up on git `add`'s interactive tag and please feel free to explore them in your own time. It seems like a bit long-winded when you do it the first time, but after a few times, it feels very straightforward and natural.

Hope it helps.
