---
layout: post
title: 'Grep, Sed and Grasp: Replace strings in files'
---

This week, I was refactoring some of the Javascript code, which involved renaming files, and then amending the code that was requiring those files.
The project uses requirejs, so the filename is kinda pivotal. I had read about [Grasp](http://graspjs.com) and saw this as an opportunity to do some refactoring voodoo. Grasp is very powerful and there is ample documentation, but when you don't have enough time, you want to look at some examples that tell you exactly what to do. Rails API docs have spoiled me for good. Grasp still needs to be conquered, perhaps another time.

Here's the one-liner that I used to accomplish this task. I used it as part of a script so the values were dynamically substituted:

 ```
 grep -rl '<oldstring>' <path> | xargs sed -i '' 's/<oldstring>/<newstring>/g' $1
 ```

`<oldstring>` is the string you want to replace

`<newstring>` is the string you want to replace `<oldstring>` with

`<path>` is where you want grep to start working from

Grep recursively - `-r` finds the files and `-l` pipes the file path in to xargs - which executes the sed command for file it receives. `$1` references the file path received via `xargs`.
This one-liner doesn't create a backup file for every file changed, however, if you want to create a backup file as well in the same directory as the file changed, you can use the following,
slightly different one-liner:

```
grep -rl '<oldstring>' <path> | xargs sed -i.bak 's/<oldstring>/<newstring>/g' $1
```

If I knew `grasp` well, I'd have used that instead, but for now, `grep` and `sed` are good enough.
