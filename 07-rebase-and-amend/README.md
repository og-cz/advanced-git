# Rebase and Amend

- [REBASE](#rebase)
  - [amend a commit](#amend-a-commit)
  - [commits cant be edited!](#commits-cant-be-edited)
  - [what is rebase anyway?](#what-is-rebase-anyway)
  - [rebase: rewinding HEAD](#rebase-rewinding-head)
  - [rebase: apply new commits](#rebase-apply-new-commits)
  - [merge vs rebase](#merge-vs-rebase)
  - [power of rebasing - replaying commits](#power-of-rebasing---replaying-commits)
  - [interactive rebase (rebase -i or rebase - -interactive)](#interactive-rebase-rebase--i-or-rebase---interactive)
  - [rebase option](#rebase-option)
  - [example rebase](#example-rebase)
  - [tip: use rebase to split commits](#tip-use-rebase-to-split-commits)
- [FIXUP AND AUTOSQUASH](#fixup-and-autosquash)
  - [tip: “ammend” any commit with fixup and autosquash!](#tip-ammend-any-commit-with-fixup-and-autosquash)
  - [rebase --exec (execute a command)](#rebase---exec-execute-a-command)
  - [abort](#abort)
  - [rebase pro tip](#rebase-pro-tip)
  - [rebase advantages](#rebase-advantages)
  - [commit early & often vs good commits](#commit-early--often-vs-good-commits)
  - [warning: never rewrite public history!](#warning-never-rewrite-public-history)
- [COMMAND SUMMARY](#command-summary)
  - [Interactive Rebase Options](#interactive-rebase-options)
  - [Merge vs Rebase](#merge-vs-rebase-1)
  - [Common Rebase Workflows](#common-rebase-workflows)
  - [Quick Tips](#quick-tips)

## REBASE

### amend a commit

- amend is a quick and easy shorcut that lets you make changes to the previous commit

![image.png](attachment:0ac2cd45-c9cf-4ec4-884e-faa2820818f7:image.png)

- but why is SHA same? because commits cant be edited

### commits cant be edited!

- remember, commit cant be edited!
- a commit is referenced by the SHA of all its data

- even if the tree the commit points to is the same, and the author is the same, the date is still different

![image.png](attachment:0cfa5433-8ec8-494a-81de-efe2c4ee7af1:image.png)

![image.png](attachment:af20f04b-694c-43b7-82ae-b086d246e35d:image.png)

- basically we just remove the previous commit and add with the new commit pointing to the HEAD branch

## REBASE

### what is rebase anyway?

- It updates your branch to match the latest version (like syncing),
  but instead of deleting or overwriting your work,
  it replays your changes on top of the new base
- 🧱 **Merge:** “Combine both sets of changes together” (keeps both histories).
- 🔄 **Rebase:** “Move my work to the latest version, like I started fresh from there.”

Rebase means give a commit a new parent

### rebase: rewinding HEAD

![image.png](attachment:667cf60c-1d89-4cde-abe2-0d4d82a6bf75:image.png)

It means Git is doing this:

1. **Temporarily moves your branch pointer (HEAD)** back to the base commit — like “rewinding” history.
2. **Re-applies (replays)** your commits _one by one_ on top of the new base.

So:

- It “rewinds” to undo your commits,
- Then “replays” them with new parents (creating new SHAs).

### rebase: apply new commits

![image.png](attachment:8e68c49e-7833-40e4-b4bb-317074b887aa:image.png)

- and we created a copy of the parent commit on the child which is tech_posts which makes it paste the newest changes on master and makes resolving much easier in terms of discompability of merging branches

### merge vs rebase

![image.png](attachment:35e5ed8d-39be-458a-9306-4265f0c22721:image.png)

- Merge = combine histories
  - **“I want Git to remember exactly how it happened.”**
- Rebase = rewrite history to look cleaner
  - **“I want history to look like I always worked on the latest version.”**

### power of rebasing - replaying commits

- commits can be:
  - edited
  - removed
  - combined
  - re-ordered
  - insterted
- before they`re repalced on top of he new HEAD

### interactive rebase (rebase -i or rebase - -interactive)

- interactive rebase opens an editor with a list of “todos”
  - in the format of: <command> <commit> <commit msg>
  - git will pick the commits in the specified order, or stop to take an action when editing or a conflict occurs
- interactive rebase with a shorcut:
  - git rebase -i <commit_to_fix>^
  - (the ^ specifies the parent commit)

### rebase option

- pick → keep this commit
- reword → keep the commit, just change the message
- edit → keep the commit, but stop to edit more than the message
- squash → combine this commit with the previous one. Stop to edit the message
- fixup → combine this commit with the previous one. keep the previous commit message
- exec → run the command on this line after pickin the previous commit -
- drop → remove the commit (tip: if u remove this line, the commit will be dropped too!)

### example rebase

![image.png](attachment:8c7a32b4-7184-4284-ada0-21d1bf8fe1de:image.png)

### tip: use rebase to split commits

editing a commit can also split it up into multiple commits!

1. start an interactive rebase with rebase -i
2. mark the commit with an edit
3. git reset HEAD^
4. git add
5. git commit
6. repeat (4) & (5) until the working area is clean!
7. git rebase - -continue

## FIXUP AND AUTOSQUASH

### tip: “ammend” any commit with fixup and autosquash!

what if we want to ammend an any commit?

1. git add new files
2. git commit —fixup <sha>
   1. this creates a new commit, the message starts with ‘fixup!’
3. git rebase -i - -autosquash <sha>^
4. git will generate the right todos for you! just save and quit

   ![image.png](attachment:c30eb20d-1ef9-4087-a952-17c0d7ad2e16:image.png)

   ![image.png](attachment:250ca72b-b32e-4a8b-97ad-8b03e985db74:image.png)

### rebase - -exec (execute a command)

git rebase -i - -exec “run-tests” <commit>

2 options for exec:

1. add it as a command when doing interactive rebase
2. use it as a flag when rebasing

- when used as a flag, the command specified by exec will run after every commit is applied
- this cant be used to run test
- the rebase will stop if the command fails, giving you a chance to fix what`s wrong

### abort

at any time before rebase is done, if things are going wrong:

- git rebase - -abort

### rebase pro tip

- before you rebase/fixup/squash/reorder:
- make a copy of your current branch:
  - git branch branch_backup
- git branch will make a new branch. without switching to it
- if rebase “succeeds” but you messed up…
- git reset branch_backup - -hard
- you`re back in business!

### rebase advantages

- rebase is incredibilty powerful
- you can slice and dice your git history
- it easy to fix previous mistakes in code
- you can keep ur git history neat and clean

### commit early & often vs good commits

- git best practices:
  - “commit often, perfect later, publish once”
- when working locally:
  - commit whenever you make changes!
  - it`ll help you be a more productive developer
- before pushing work to a shared repo:
  - rebase to clean up the commit history

### warning: never rewrite public history!

- rebase commits are copes
- if other people are wokring on the same repo they would be workign on different commits
- you could cause massive merge conflicts
- even worse, you can cause people to lose their work!

## COMMAND SUMMARY

Rebasing, Editing, Squashing, and Cleaning Up History

| Command / Concept                                     | Description                                                                                                     |
| ----------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **`git rebase <branch>`**                             | Replays your current branch’s commits on top of another branch (like starting from the latest version).         |
| **`git rebase -i <commit>^`**                         | Starts an _interactive rebase_ from the parent of `<commit>` — lets you edit, reorder, squash, or drop commits. |
| **`git rebase --continue`**                           | Continues the rebase after resolving conflicts or finishing manual edits.                                       |
| **`git rebase --abort`**                              | Cancels the rebase and returns to the branch’s original state before rebasing.                                  |
| **`git rebase --skip`**                               | Skips the current commit during rebase (used when a commit cannot be applied cleanly).                          |
| **`git rebase --onto <newbase> <upstream> <branch>`** | Advanced: rebase a specific range of commits from `<branch>` onto a new base.                                   |
| **`git rebase --interactive`** _(or `-i`)_            | Opens a text editor with a list of commits to pick, edit, squash, fixup, etc.                                   |
| **`git rebase --exec "<command>"`**                   | Runs a shell command (like tests) after each commit is applied during rebase.                                   |
| **`git commit --amend`**                              | Rewrites the **last commit** (e.g., to fix message or add forgotten files). Creates a _new_ SHA.                |
| **`git commit --fixup <sha>`**                        | Creates a temporary “fixup!” commit meant to be merged (autosquashed) into the target commit.                   |
| **`git rebase -i --autosquash <sha>^`**               | Automatically places `fixup!` and `squash!` commits in order during interactive rebase.                         |
| **`git branch branch_backup`**                        | Create a safety backup before rebasing — restore later with `git reset branch_backup --hard`.                   |

---

### Interactive Rebase Options

| Option   | Description                                                                   |
| -------- | ----------------------------------------------------------------------------- |
| `pick`   | Keep this commit as-is.                                                       |
| `reword` | Keep the commit but edit the commit message.                                  |
| `edit`   | Stop and allow manual edits or additional changes.                            |
| `squash` | Combine this commit with the previous one; edit combined message.             |
| `fixup`  | Combine this commit with the previous one; keep the previous message.         |
| `exec`   | Run the specified shell command after the commit.                             |
| `drop`   | Remove the commit entirely from history. _(Removing the line also drops it.)_ |

---

### Merge vs Rebase

| Action     | Keeps Both Histories? | Rewrites History? | Creates New Commits? | Use When                                                                    |
| ---------- | --------------------- | ----------------- | -------------------- | --------------------------------------------------------------------------- |
| **Merge**  | ✅ Yes                | ❌ No             | ✅ Merge commit      | You want to preserve exact history of all branches.                         |
| **Rebase** | ❌ No                 | ✅ Yes            | ✅ New SHAs          | You want a clean, linear history as if all work started on the latest base. |

---

### Common Rebase Workflows

| Goal                                            | Command                                                                                                           |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Sync your feature branch to the latest `main`   | `git fetch origin && git rebase origin/main`                                                                      |
| Rewrite messy commits before pushing            | `git rebase -i HEAD~5`                                                                                            |
| Amend an earlier commit (not just the last one) | `git commit --fixup <sha>` → `git rebase -i --autosquash <sha>^`                                                  |
| Split one commit into several                   | `git rebase -i <commit>^` → mark `edit` → `git reset HEAD^` → `git add/commit` in steps → `git rebase --continue` |
| Skip a problematic commit                       | `git rebase --skip`                                                                                               |
| Abort a rebase completely                       | `git rebase --abort`                                                                                              |

---

### Quick Tips

| Situation                                 | Recommended Command               |
| ----------------------------------------- | --------------------------------- |
| Make a backup before risky rebase         | `git branch branch_backup`        |
| Restore after a bad rebase                | `git reset branch_backup --hard`  |
| Test each commit during rebase            | `git rebase -i --exec "npm test"` |
| Clean up local commit history before push | `git rebase -i HEAD~N`            |
| Avoid rewriting shared commits            | ❌ Don’t rebase public branches!  |
