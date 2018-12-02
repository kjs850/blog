---
title: git squash
---
date: 2018-12-02 20:26:59

## 준비
```bash
 jake.ko  ~/Dev  cd git-study
 jake.ko  ~/Dev/git-study  ll
 jake.ko  ~/Dev/git-study  git init
Initialized empty Git repository in /Users/jake.ko/Dev/git-study/.git/
 jake.ko  ~/Dev/git-study   master  ll
 jake.ko  ~/Dev/git-study   master  ll -alr
total 0
drwxr-xr-x  10 jake.ko  staff   320B 12  2 20:21 .git
drwxr-xr-x  22 jake.ko  staff   704B 12  2 20:16 ..
drwxr-xr-x   3 jake.ko  staff    96B 12  2 20:17 .
 jake.ko  ~/Dev/git-study   master  echo first > first.txt
 jake.ko  ~/Dev/git-study   master  git add .
 jake.ko  ~/Dev/git-study   master ✚  git commit -m "A"
[master (root-commit) 20611a0] A
 1 file changed, 1 insertion(+)
 create mode 100644 first.txt
 jake.ko  ~/Dev/git-study   master  echo second > second.txt
 jake.ko  ~/Dev/git-study   master  git add .
 jake.ko  ~/Dev/git-study   master ✚  git commit -m "B"
[master 381d030] B
 1 file changed, 1 insertion(+)
 create mode 100644 second.txt
 jake.ko  ~/Dev/git-study   master  echo third > third.txt
 jake.ko  ~/Dev/git-study   master  git add .
 jake.ko  ~/Dev/git-study   master ✚  git commit -m "C"
[master 52bfd68] C
 1 file changed, 1 insertion(+)
 create mode 100644 third.txt
 jake.ko  ~/Dev/git-study   master 
```
## git log
```bash
commit 52bfd68372367dcbb2b4c1c5bb1ddb1086f02119 (HEAD -> master)
Author: jake.ko <jake.ko@kakaocorp.com>
Date:   Sun Dec 2 20:23:30 2018 +0900

    C

commit 381d030dafd61153bb3754c260b7216a9b5c47e9
Author: jake.ko <jake.ko@kakaocorp.com>
Date:   Sun Dec 2 20:22:52 2018 +0900

    B

commit 20611a043cea164d8d3e5f5d73b3949974a5fe50
Author: jake.ko <jake.ko@kakaocorp.com>
Date:   Sun Dec 2 20:22:19 2018 +0900

    A

```
## git rebase -i HEAD~2
```bash
pick 381d030 B
pick 52bfd68 C

# Rebase 20611a0..52bfd68 onto 20611a0 (2 commands)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out




```
## 바꾸고 저장
```bash

pick 381d030 B
squash 52bfd68 C
```

## 아래와 같은 수정이 가능 , 디폴트 그대로 저장 (.git/COMMIT_EDITMSG)
```bash
# This is a combination of 2 commits.
# This is the 1st commit message:

B

# This is the commit message #2:

C

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sun Dec 2 20:22:52 2018 +0900
#
# interactive rebase in progress; onto 20611a0
# Last commands done (2 commands done):
#    pick 381d030 B
#    squash 52bfd68 C
# No commands remaining.
# You are currently rebasing branch 'master' on '20611a0'.
#
# Changes to be committed:
#       new file:   second.txt
#       new file:   third.txt
#
```

## 결과 
```bash
jake.ko  ~/Dev/git-study   master  git rebase -i HEAD~2
[detached HEAD 6899e57] B
 Date: Sun Dec 2 20:22:52 2018 +0900
 2 files changed, 2 insertions(+)
 create mode 100644 second.txt
 create mode 100644 third.txt
Successfully rebased and updated refs/heads/master
```

## git log
```bash
'git help -a' and 'git help -g' list available subcommands and some
commit 6899e57839eb085a8f0188572aec93ab1b8db74b (HEAD -> master)
Author: jake.ko <jake.ko@kakaocorp.com>
Date:   Sun Dec 2 20:22:52 2018 +0900

    B

    C

commit 20611a043cea164d8d3e5f5d73b3949974a5fe50
Author: jake.ko <jake.ko@kakaocorp.com>
Date:   Sun Dec 2 20:22:19 2018 +0900

    A
(END)
```




tags: [git]
