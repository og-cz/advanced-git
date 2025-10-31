### Step 1 - Amend a Commit

Create two new files, first.txt and second.txt, then commit the first but not the second:

```bash
# checkout exercise7
1. Asus@/07-rebase-and-amend (main)
$ git checkout exercise7
M       README.md
Switched to branch 'exercise7'

# create first file
2. Asus@/07-rebase-and-amend (exercise7)
$ echo "this is first file" > first.txt
this is first file first.txt

# create second file
3. Asus@/07-rebase-and-amend (exercise7)
$ echo "this is second file" > second.txt
this is second file second.txt

4. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git add first.txt
warning: in the working copy of '07-rebase-and-amend/first.txt', LF will be replaced by CRLF the next time Git touches it

# commit the first.txt but not included second
5. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git commit -m "commited two new files"
[exercise7 1d0029b] commited two new files
 1 file changed, 1 insertion(+)
 create mode 100644 07-rebase-and-amend/first.txt

# check status
6. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git status
Untracked files:
        second.txt
```

Oh no, we forgot to include the second file in our commit. No worries, as long as we haven't pushed our commit to a remote repository (like origin), we can amend the last commit to include the other file.

```bash
# add second.txt
7. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git add second.txt

# ammend -> commit the new child changes to its parent
8. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git commit --amend
hint: Waiting for your editor to close the file...
## after editing
$ git commit --amend
[exercise7 cc96feb] commited two new files
 Date: Fri Oct 31 12:25:01 2025 +0800
 2 files changed, 2 insertions(+)
 create mode 100644 07-rebase-and-amend/first.txt
 create mode 100644 07-rebase-and-amend/second.txt
```

There we go, we've fixed the commit to contain both first.txt and second.txt. Notice that the SHAs are different between the original commit and the amended commit . Commits can't be edited, so a new commit with the changed data was created and the old commit was replaced.

### Step 2 - Set up for a Rebase

Let's get things set up for a simple rebase demo. Checkout master, and let's pretend that we have a new feature branch, called exercise7-2.

```bash
# checkout branch of main
10. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git checkout main
M       README.md
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

# checkout and switch to that branch
11. Asus@ MINGW64 07-rebase-and-amend (main)
$ git checkout -b exercise7-2
Switched to a new branch 'exercise7-2'

# check all log in oneline
12. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git log --oneline
3cc8c7c (HEAD -> exercise7-2, origin/main, origin/HEAD, main) advanced-git
f96cafe advanced-git description?
934ce4a (origin/exercise6, exercise6) advanced-git
```

Now let's create a new feature and commit it to our feature branch:

```bash
# switch branch
13. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git checkout main

# The double arrow >> means 'append' to the file instead of overwrite.
14. Asus@ MINGW64 07-rebase-and-amend (main)
$ echo "master is changing ahead" >> hello.txt

# adding hello
15. Asus@ MINGW64 07-rebase-and-amend (main)
$ git add hello.txt
warning: in the working copy of '07-rebase-and-amend/hello.txt', LF will be replaced by CRLF the next time Git touches it

# commit hello.txt on main branch
16. Asus@ MINGW64 07-rebase-and-amend (main)
$ git commit -m "master has changed"
[main 1dfcff7] master has changed
 1 file changed, 1 insertion(+)
 create mode 100644 07-rebase-and-amend/hello.txt
```

Switching back to our feature branch. It's a good idea to periodically merge in the master branch, to keep things up to date and minimize the number of conflicts when the feature branch is eventually merged into master. Instead of creating unsightly merge commits though, let's use rebase to replay our feature commits on top of master's commits.

````bash
17. Asus@ MINGW64 07-rebase-and-amend (main)
$ git checkout exercise7-2
M       README.md
Switched to branch 'exercise7-2'

# see all commit in oneline
18. Asus@ MINGW64 07-rebase-and-amend (main)
$ git log --oneline
1dfcff7 (HEAD -> main) master has changed

# REBASING FROM MAIN
19. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git rebase main
Successfully rebased and updated refs/heads/exercise7-2.

# see all commit in oneline
20. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git log --oneline
6ed83d9 (HEAD -> exercise7-2, origin/main, origin/HEAD, main) master has changed

# check status
21. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git status
On branch exercise7-2
nothing to commit, working tree clean

# create new commit here
22. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ echo "hi" > hi.txt

# add and commit hi.txt
23. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git commit -m "added hi.txt"
[exercise7-2 350ff6b] added hi.txt
 1 file changed, 1 insertion(+)
 create mode 100644 hi.txt

# check new changes
24. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git log --oneline
350ff6b (HEAD -> exercise7-2) added hi.txt
6ed83d9 (origin/main, origin/HEAD, main) master has changed

# go back to master
25. ### Step 1 - Amend a Commit

Create two new files, first.txt and second.txt, then commit the first but not the second:

```bash
# checkout exercise7
1. Asus@/07-rebase-and-amend (main)
$ git checkout exercise7
M       README.md
Switched to branch 'exercise7'

# create first file
2. Asus@/07-rebase-and-amend (exercise7)
$ echo "this is first file" > first.txt
this is first file first.txt

# create second file
3. Asus@/07-rebase-and-amend (exercise7)
$ echo "this is second file" > second.txt
this is second file second.txt

4. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git add first.txt
warning: in the working copy of '07-rebase-and-amend/first.txt', LF will be replaced by CRLF the next time Git touches it

# commit the first.txt but not included second
5. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git commit -m "commited two new files"
[exercise7 1d0029b] commited two new files
 1 file changed, 1 insertion(+)
 create mode 100644 07-rebase-and-amend/first.txt

# check status
6. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git status
Untracked files:
        second.txt
````

Oh no, we forgot to include the second file in our commit. No worries, as long as we haven't pushed our commit to a remote repository (like origin), we can amend the last commit to include the other file.

```bash
# add second.txt
7. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git add second.txt

# ammend -> commit the new child changes to its parent
8. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git commit --amend
hint: Waiting for your editor to close the file...
## after editing
$ git commit --amend
[exercise7 cc96feb] commited two new files
 Date: Fri Oct 31 12:25:01 2025 +0800
 2 files changed, 2 insertions(+)
 create mode 100644 07-rebase-and-amend/first.txt
 create mode 100644 07-rebase-and-amend/second.txt
```

There we go, we've fixed the commit to contain both first.txt and second.txt. Notice that the SHAs are different between the original commit and the amended commit . Commits can't be edited, so a new commit with the changed data was created and the old commit was replaced.

### Step 2 - Set up for a Rebase

Let's get things set up for a simple rebase demo. Checkout master, and let's pretend that we have a new feature branch, called exercise7-2.

```bash
# checkout branch of main
10. Asus@ MINGW64 07-rebase-and-amend (exercise7)
$ git checkout main
M       README.md
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

# checkout and switch to that branch
11. Asus@ MINGW64 07-rebase-and-amend (main)
$ git checkout -b exercise7-2
Switched to a new branch 'exercise7-2'

# check all log in oneline
12. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git log --oneline
3cc8c7c (HEAD -> exercise7-2, origin/main, origin/HEAD, main) advanced-git
f96cafe advanced-git description?
934ce4a (origin/exercise6, exercise6) advanced-git
```

Now let's create a new feature and commit it to our feature branch:

```bash
# switch branch
13. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git checkout main

# The double arrow >> means 'append' to the file instead of overwrite.
14. Asus@ MINGW64 07-rebase-and-amend (main)
$ echo "master is changing ahead" >> hello.txt

# adding hello
15. Asus@ MINGW64 07-rebase-and-amend (main)
$ git add hello.txt
warning: in the working copy of '07-rebase-and-amend/hello.txt', LF will be replaced by CRLF the next time Git touches it

# commit hello.txt on main branch
16. Asus@ MINGW64 07-rebase-and-amend (main)
$ git commit -m "master has changed"
[main 1dfcff7] master has changed
 1 file changed, 1 insertion(+)
 create mode 100644 07-rebase-and-amend/hello.txt
```

Switching back to our feature branch. It's a good idea to periodically merge in the master branch, to keep things up to date and minimize the number of conflicts when the feature branch is eventually merged into master. Instead of creating unsightly merge commits though, let's use rebase to replay our feature commits on top of master's commits.

```bash
17. Asus@ MINGW64 07-rebase-and-amend (main)
$ git checkout exercise7-2
M       README.md
Switched to branch 'exercise7-2'

# see all commit in oneline
18. Asus@ MINGW64 07-rebase-and-amend (main)
$ git log --oneline
1dfcff7 (HEAD -> main) master has changed

# REBASING FROM MAIN
19. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git rebase main
Successfully rebased and updated refs/heads/exercise7-2.

# see all commit in oneline
20. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git log --oneline
6ed83d9 (HEAD -> exercise7-2, origin/main, origin/HEAD, main) master has changed

# check status
21. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git status
On branch exercise7-2
nothing to commit, working tree clean

# create new commit here
22. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ echo "hi" > hi.txt

# add and commit hi.txt
23. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git commit -m "added hi.txt"
[exercise7-2 350ff6b] added hi.txt
 1 file changed, 1 insertion(+)
 create mode 100644 hi.txt

# check new commit
24. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git log --oneline
350ff6b (HEAD -> exercise7-2) added hi.txt
6ed83d9 (origin/main, origin/HEAD, main) master has changed
```

```bash
25. git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

# create a new file
26. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (main)
$ echo 'bye' > bye.txt

# adding and commit bye.txt
27.
Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (main)
$ git add bye.txt
warning: in the working copy of 'bye.txt', LF will be replaced by CRLF the next time Git touches it

28. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (main)
$ git commit -m "adding bye.txt"
[main 21dac08] adding bye.txt
 1 file changed, 1 insertion(+)
 create mode 100644 bye.txt

# checkout exercise7-2
29. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (main)
$ git checkout exercise7-2
Switched to branch 'exercise7-2'

# check history
30. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git log --oneline
350ff6b (HEAD -> exercise7-2) added hi.txt
6ed83d9 (origin/main, origin/HEAD) master has changed
```

Tip: When working on a feature branch that's likely to conflict, I prefer to rebase from master often and fix conflicts as they come up. This way, I'm not stuck with a huge disastrous merge full of conflicts when I'm done with my feature and ready to merge it back to master.

### Step 3 - Interactive Rebase

Let's set up our feature branch for a very simple interactive rebase. Add another new feature and commit it:

```bash
# rebasing from main
31. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git rebase main
Successfully rebased and updated refs/heads/exercise7-2.

# check history
32. Asus@ MINGW64 ~/Documents/ogcz/_DEV/advanced-git (exercise7-2)
$ git log --oneline
321d75b (HEAD -> exercise7-2) added hi.txt
21dac08 (main) adding bye.txt
6ed83d9 (origin/main, origin/HEAD) master has changed

# created new file
33. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ echo "another feature" > another_feature.txt

# adding a file
34. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git add another_feature.txt
warning: in the working copy of '07-rebase-and-amend/another_feature.txt', LF will be replaced by CRLF the next time Git touches it

# commited the new added file
35. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git commit -m "added another_feature.txt"
[exercise7-2 24493fa] added another_feature.txt
 1 file changed, 1 insertion(+)
 create mode 100644 07-rebase-and-amend/another_feature.txt
```

Now we have two new commits on top of master.

```bash
# check last 3 commits
36. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git log -n 3 --oneline
24493fa (HEAD -> exercise7-2) added another_feature.txt
321d75b added hi.txt
21dac08 (main) adding bye.txt
```

# REAL REBASE

When we're done with our feature, we want to clean these commits up by combining them using squash, and changing the commit message using reword.

Start the interactive rebase by passing in one commit before the one you want to start rebasing from. In this case, we want to rebase commit 64db08a and the commit after it.

We have some options for which ref to use. All the options below will get the same result:

HEAD~2 - 2 commits before HEAD
321d75b^ - points to one commit back - parent 21dac08
21dac08 - the actual commit before the one we want to rebase from
main - since master points to 21dac08

```bash
37. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git rebase -i HEAD~2
hint: Waiting for your editor to close the file...

# it will open something like this
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
pick 321d75b # added hi.txt
pick 24493fa # added another_feature.txt

# Rebase 21dac08..24493fa onto 21dac08 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
....... so on
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# after we do this
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
reword 321d75b # added hi.txt
squash 24493fa # added another_feature.txt

# Rebase 21dac08..24493fa onto 21dac08 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# after it will doing that it will open something like this
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
added hi.txt

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Fri Oct 31 12:50:46 2025 +0800
#
# interactive rebase in progress; onto 21dac08
# Last command done (1 command done):
#    reword 321d75b # added hi.txt
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# we changed the commit message to this
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
added two new features here

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Fri Oct 31 12:50:46 2025 +0800
#
# interactive rebase in progress; onto 21dac08
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

# after changing commit message it will open something like this
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<
# This is a combination of 2 commits.
# This is the 1st commit message:

added two new features here

# This is the commit message #2:

############################ we just commend this one below because we dont need this second commit mensahe
# added another_feature.txt

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Fri Oct 31 12:50:46 2025 +0800
#
# interactive rebase in progress; onto 21dac08
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

38. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git rebase -i HEAD~2
[detached HEAD a49dbeb] added two new features here
 Date: Fri Oct 31 12:50:46 2025 +0800
 1 file changed, 1 insertion(+)
 create mode 100644 07-rebase-and-amend/hi.txt
[detached HEAD 62ffaac] added two new features here
 Date: Fri Oct 31 12:50:46 2025 +0800
 2 files changed, 2 insertions(+)
 create mode 100644 07-rebase-and-amend/another_feature.txt
 create mode 100644 07-rebase-and-amend/hi.txt
Successfully rebased and updated refs/heads/exercise7-2.
```

Now, take a look at your git log:

```bash
39. Asus@ MINGW64 07-rebase-and-amend (exercise7-2)
$ git log --oneline
62ffaac (HEAD -> exercise7-2) added two new features here
21dac08 (main) adding bye.txt
6ed83d9 (origin/main, origin/HEAD) master has changed
```

Like magic, our two new features have been squashed into one commit, we've reworded the commit message to show this, and our changes are sitting neatly on top of the change from the master branch.

Tip: When working on a feature branch, commit early and often to minimize the likelihood of losing work. It'll also make back tracking easier. Once I'm ready to merge my changes, I do an interactive rebase to squash commits where needed, and take the opportunity to write better commit messages.
