---
layout:     post
title:      "Learning How Git Rebase Works Pt. 1"
date:       2022-02-04 13:28:00
author:     "bobby"
tags:       programming git
---

# Intro

According to github, the first branch I've ever made was 11 years ago. This means I have been
using git for about 10-11 years now. And you know what? I still don't really know when and how to
use git rebase. That ends today.

# Motivation to learning Git Rebase

Historically, I've always used the "merge" command because it was what I learned first and what I
was familiar with. If I needed to pull any remote changes from master, I would do a `git pull`, which does a `git fetch`
followed by a `git merge`. 

One day I was pair programming with a co-worker and I saw that they used the --rebase flag like this:

```
git pull --rebase origin master
```

So I asked, "Why rebase?"

And they responded, "So the commit history is cleaner"

# The difference between merge and rebase

If you have a master branch and make commits to it, the history would look something like this:

```
A --> B --> C
```

Lets say you make a feature-branch and make a commit. The history would look something like this

```
A --> B --> C # master branch
             \
              D # feature branch
```

And then you add a few more commits, the history looks something like this:

```
A --> B --> C # master branch
             \
              D --> E --> F # feature branch
```

But while this is happening, you have another person contributing to the master branch of the repository.

```
A --> B --> C --> G --> H --> I # master branch
             \
              D --> E --> F # feature branch
```

So now you want to add those commits from the feature branch back on to your master branch. Do you you do a `git merge` or a `git rebase`?

## If you do a git merge

If you decide to do a git merge, the commit history will look something like this: 

```
A --> B --> C --> G --> H --> I --> J (merge commit)    # master branch
             \                     /
              D --> E --> F ------  # feature branch
```

The commit designated as "J" in the example above is what is called a "merge commit."
Because the history between these two branches started to diverge at commit "C", Git
will attempt to reconcile the history. As a result, commit "J" will have have two parent commits.
An example of what the history would look like in the git logs is something like this:

```
Merge: b0b1484 d4b259c
Date:   Wed Feb 16 22:42:35 2022 -0800

    COMMIT J (fix merge conflict)

commit b0b148458ce2942b5fdf47aad3646a2c2638d16a
Date:   Wed Feb 16 22:42:07 2022 -0800

    COMMIT I

commit d4b259c3b92090bb206bc3f1d8674bcb2a675e1e (feature-branch-1)
Date:   Wed Feb 16 22:41:35 2022 -0800

    COMMIT F

commit 1439cfb0fee44fac60ee0d721d4d851851368fca
Date:   Wed Feb 16 22:41:20 2022 -0800

    COMMIT H

commit c97a68886ac144fe285f8b7efa00b70d47912dfd
Date:   Wed Feb 16 22:40:36 2022 -0800

    COMMIT E

commit 3f5029191091a5d0a633e724f468598bed2d8058
Date:   Wed Feb 16 22:40:15 2022 -0800

    COMMIT G

commit f6695865da51265d95e7db6d2ef0ef69ef5a46e7
Date:   Wed Feb 16 22:39:24 2022 -0800

    COMMIT D

commit f939414c7261d3e2386c01a16e94ae73e97ed652
Date:   Wed Feb 16 22:38:46 2022 -0800

    COMMIT C

commit a7150bd03908df2d5619047c1e15be5395b7ecfb
Date:   Wed Feb 16 22:38:37 2022 -0800

    COMMIT B

commit 8a0d2923f99d41d5f24f4055ae32e1d80e76e3f5
Date:   Wed Feb 16 22:38:28 2022 -0800

    COMMIT A

---
```


As you can see, the commit history looks a bit staggered. The feature-branch had commits "G", "H"
and "I", and after doing a git merge, git will order those commits in the order they were done by time, so commits G, H, and I won't be in the sequence and order they were committed while working on the feature branch.

## If you do a git rebase

Rebase will take your commits of your feature branch and "replay them" _on top_ of the branch
you are rebasing on.
If you do a rebase, the history will look like it will have a linear history like this:

```
A --> B --> C --> G --> H --> I --> J --> D --> E --> F 
```

Example logs:

```
commit 63e3bd94da035644b8e6cc625dbc09d2fda21f2e (HEAD -> master, rebase-branch)
Date:   Wed Feb 16 22:54:00 2022 -0800

    COMMIT F

commit dfa08724626ed3d1d5e6e42e9a75bf0a9e47d39d
Date:   Wed Feb 16 22:53:51 2022 -0800

    COMMIT E

commit 26b92f333c13f27da1b5295597997aa39f418478
Date:   Wed Feb 16 22:53:31 2022 -0800

    COMMIT D

commit 579cbd6e385474db5449f94bad974842627ebace
Date:   Wed Feb 16 22:55:16 2022 -0800

    COMMIT I

commit 3ed4e3bbe95d28a209b8968e492b63e5fb5125ec
Date:   Wed Feb 16 22:54:51 2022 -0800

    COMMIT H

commit 2cd4e72f97b27b4b122fafe2c83c36d619d441da
Date:   Wed Feb 16 22:54:27 2022 -0800

    COMMTI G

commit 5e34d0cbf8d84c4ab1b81084145ace837f32f0fb
Date:   Wed Feb 16 22:52:23 2022 -0800

    COMMIT C

commit 41177e96ec5f16c9575e190fc5eca899abc1c716
Date:   Wed Feb 16 22:52:07 2022 -0800

    COMMIT B

commit bf12c970b545ade05f18ff63733bc280acb74ae9
Date:   Wed Feb 16 22:51:48 2022 -0800

    COMMIT A
```

## Conclusion

I think there are several factors that determine which type of git workflow to use.
Some devs like preserving the true history of what happens in the codebase, so they will
be okay with using git merge. Others like to keep a clean, linear history, which then
they will use the rebase command. There are some other considerations to take when
using merge vs rebase. If you are working on a branch with someone else, becareful
when using git rebase as it can alter history. If you alter the history of your
shared branch and push it back to Github, its possible you can erase history
or create a bad state for the others who are also working in the same branch.



