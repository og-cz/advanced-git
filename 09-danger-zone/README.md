# Danger Zone

## Local Destructive Operations

- **git checkout - -<file>**
  - if the file is presnet in the staging area, it`ll be overwritten.
- **git reset - -hard**
  - will overwrite changes that are staged and in the working area
- unless changes are stashed, there`s no way of getting them back!
- tip: use **git stash - -include-untracked** to include working area changes in your stash

## Remote Destructive Operations - Rewriting History

- there are many operations that can rewrite history:
  - **rebase**
  - **amend**
  - **reset**
- if your code is hosted or shared:
  - **Never run git push -f**

## Recover Lost Work

- use ORIG_HEAD
  - `ORIG_HEAD` is basically a **special, automatic save point**
  - “Hmm, you’re about to do something that could rewrite history, lose commits, or change your branch pointer let me drop a bookmark real quick”
- the commit HEAD was pointing before a:
  - reset
  - merge
- check for repository copies:
  - github
  - coworker

## ORIG_HEAD to undo a merge

- use ORIG_HEAD to undo merges
- git reset - -merge ORIG_HEAD
- use - -merge flag to preserve any uncommited changes
  ![image.png](attachment:4d7d11f5-77ce-4955-8de8-357ee86bac14:image.png)

## Using GIT Reflog and ‘@’ Syntax

- by default, git keeps commits around for about 2 weeks
- if you need to go back in time, and find a commit thats no longer referenced, you can look in the reflog
- the syntax of reflog is different
  - HEAD@{2} means “the value of HEAD 2 moves ago”
