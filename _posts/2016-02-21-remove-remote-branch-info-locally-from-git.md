---
layout: post
title: Remove remote branch info locally from git
---

You use git for version control.

You got a new feature to write.

You do the work and push your work into a new feature branch.

Open a PR for your work either on BitBucket or GitHub or anything else.

PR gets merged and the remote branch is deleted.

But, wait, you have the remote repository still listing locally when you run: `git branch -r`

Now, I don't want it. Once the branch has been disposed of remotely, it has no business on the local machine.

There are two ways to get rid of it.

1. Remove all remote branches deleted remotely with this command: `git remote update origin --prune`

1. Remove just one branch locally: `git remote prune my-new-feature`

There is however a subtle difference in the two, i.e. you can pass options to the latter command to execute a dry run before actually doing it, like the command below:

```
git remote prune -n my-new-feature
```

Hope it helps!
