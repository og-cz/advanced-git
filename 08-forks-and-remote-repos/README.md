# Forks and Remote Repos

- [Forks and Remote Repos](#forks-and-remote-repos)
  - [GITHUB VS GIT](#github-vs-git)
    - [distributed version control system](#distributed-version-control-system)
    - [github vs git - the key is collaboration](#github-vs-git---the-key-is-collaboration)
  - [REMOTES](#remotes)
    - [clone repository](#clone-repository)
    - [viewing remotes](#viewing-remotes)
    - [cloned someone else's repository](#cloned-someone-elses-repository)
  - [FORKS, PULL REQUESTS, & UPSTREAMS](#forks-pull-requests--upstreams)
    - [fork](#fork)
    - [merging changes to original project from a fork](#merging-changes-to-original-project-from-a-fork)
    - [staying up to date](#staying-up-to-date)
  - [GITHUB WORKFLOW](#github-workflow)
    - [triangular workflow](#triangular-workflow)
    - [tracking branches](#tracking-branches)
    - [fetch](#fetch)
    - [pull](#pull)
    - [push](#push)
    - [git pull --rebase](#git-pull---rebase)
    - [git pull vs git pull --rebase](#git-pull-vs-git-pull---rebase)
    - [note: tag](#note-tag)
    - [contributing to open source projects with pull request](#contributing-to-open-source-projects-with-pull-request)
    - [advice](#advice)
    - [pushing/merging your changes back to a remote](#pushingmerging-your-changes-back-to-a-remote)

## GITHUB VS GIT

### distributed version control system

![image.png](attachment:54ce643b-5705-4c7c-a8f3-ca49330fb0fa:image.png)

before git older system like CVS, SVN had one central repository, one master server eveyrone will push through it

by doing with that central repo, SVN is down we could do anything

and git doesnt do taht way, bcs of the efficiency how git save data, compression, and interesring algorihtm, we can store our git in our own repo without needing network unless our code is huge

intereseting story were microsoft uses a git repo and its so huge and old they run into problems. so unless we are reunning like windows i guess a smal project is fine

### github vs git - the key is collaboration

- git
  - open soruce version control software
- github:
  - repository hosting
  - browse code
  - issues
  - pull request
  - forks

## REMOTES

- a remote is a git repository stored elsewhere - on the web, github, etc.
- **origin** is the default name git gives to the server you cloned from.
- cloning a remote repository from a URL will fetch the whole repository. and makes a local copy in yout .git folder
- you may have different priveleges for a remote
  - read/write for some, read only for others

### clone repository

![image.png](attachment:d4475797-4db6-4143-b709-2cc3d71e49d0:image.png)

- its basically just installing a remote repository to local
- by defaulti ts a operation of downloading

### viewing remotes

![image.png](attachment:b5a03469-603d-45b9-a870-127a458b965b:image.png)

### cloned someone else`s repository

![image.png](attachment:313e59d6-391f-4117-bae4-5a143f415f33:image.png)

## FORKS, PULL REQUESTS, & UPSTREAMS

### fork

![image.png](attachment:309edeef-7e62-4b61-a6dc-7f3af56406a3:image.png)

- a fork is a copy of a repository that`s stored in your github account
- you can clone your fork to your local computer

### merging changes to original project form a fork

![image.png](attachment:05b99a30-7ef3-477f-ae72-f88ba069647c:image.png)

- pull request is a way to merge our code in the forked codebase
- its liek saying knock knock i fix this bug can u please accept the changes?

### staying up to date

- while you work on you fork, other changes are getting merged into the source repository
- in order to stay up to date, set up an upstream
- by adding an upstream remote, you can pull down changes that have been added to the original repository after you forked it.
  ![image.png](attachment:8fcada97-4e09-4106-a6dc-f7c0e5725cc4:image.png)

## GITHUB WORKFLOW

### triangular workflow

![image.png](attachment:d5f95b1b-1dab-411e-b602-0f00ad5f0d6c:image.png)

### tracking branches

- track a branch to tie it to an upstream branch
  - bonus: use git push/pull with no arguments
- to checkout a remote branch, with tracking:
  - git checkout -t origin/feature
- tell git which branch to track first time you push:
  - git push **_-u/—set-upstream_** origin feature

![image.png](attachment:9061126d-9d64-45a8-bf73-05aed460eb42:image.png)

- git branch -vv → shows which upstream or remote branhc we are tracking in our local branch and also shows how many commits it behind

### fetch

- git fetch is important for keeping you local repository up to date with a remote
- it pulls down all the changes that happened on the server
- but, it doesn`t change your local repository!

### pull

- pulling will pull down the changes from the remote repository to your local repository, and merging them with a local branch
- under the hood:
  - git pull = **git fetch && git merge**
- if changes happened upstream, git will create a merge commit
- otherwise, it will fast-forward

### push

- pushing sends your changes to the remote repository
- git only allows you to push if your changes won`t cause a conflict
- tip:
  - to see commits which havent been pushed upstream yet, use:
  - git cherry -v

### git pull - -rebase

- git pull - -rebase will fetch, update your local branch to copy the upstream branch, the nreplay any commits you made via rebase
- bonus: when you open a PR, there will be no unsightly merge commits!

### git pull vs git pull - -rebase

![image.png](attachment:9f9027b9-8feb-4964-b62c-1c18f37d4f07:image.png)

- same idea of rebase nad merge , git pull is a merge by default, but doing git pull rebase is just a decision if we want to make another commit which is seperate from the other branch or combine as a whole commit using rebase

### note: tag

- git doesn`t automatically push local tags to a remote repository
- to push tags:
  - git push <tagname>
  - git push - -tags

### contributing to open soruce projects with pull request

- before opening a PR:
  - keep commit history clean and neat. Rebase if needed
  - run projects tests on your code
  - pull in Upstream changes (preferably via rebase to avoid merge commits)
  - check for a CONTRIBUTING (.md/.txt) in the project root
- after opening a PR:
  - explain your changes very thoroughly in the pull request
  - link to any open issues that your pull request might fix
  - check back for comments from the maintainers

### advice

- encourage developers to work on their own forks of a repository
- mistakes are less likely to happen if no one is puhsing directly to the “source of truth” for your codebase!
- you can rebase and force push freely to your own origin, as long as no one lese is cloning your branch

### pushing/merging you changes back to a remote

- rule of thumnb
  - rebase commits on your local feature branch
  - merge feature branches back to origin (or upstream)
- when accepting a pull request
  - squash and merge or rebase with care
  - you’ll lose context about the work on the feature branch!
  - it’ll make it harder to debug when issues arise in the future
