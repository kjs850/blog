---
title: git-flow
---
date: 2019-02-07 18:38:24

## 설치
기존 git 저장소 내에서 초기화하는 것으로 git-flow의 사용을 시작합니다
```bash
> git flow init
Initialized empty Git repository in /Users/jake.ko/Dev/git-flow-test/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []
>
>ll
total 0
drwxr-xr-x  25 jake.ko  staff  800  2  7 18:01 ..
drwxr-xr-x   3 jake.ko  staff   96  2  7 18:36 .
drwxr-xr-x  13 jake.ko  staff  416  2  7 18:36 .git
```
몇몇 질문에 대답해서 브랜치의 명명규칙을 정합니다. 기본 값을 사용하기를 권장합니다.

## 새 기능 시작
```bash
> git flow feature start MYFEATURE
Switched to a new branch 'feature/MYFEATURE'

Summary of actions:
- A new branch 'feature/MYFEATURE' was created, based on 'develop'
- You are now on branch 'feature/MYFEATURE'

Now, start committing on your feature. When done, use:

     git flow feature finish MYFEATURE

> git status
On branch feature/MYFEATURE
nothing to commit, working tree clean

> echo 'my feature' > myfeature.txt
> git add .
> git commit -m"add myfeature"
```

## 기능 완료
```bash
 jake.ko  ~/Dev/git-flow-test   feature/MYFEATURE  git flow feature finish MYFEATURE
Switched to branch 'develop'
Updating f68a50c..102c09d
Fast-forward
 myfeature.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 myfeature.txt
Deleted branch feature/MYFEATURE (was 102c09d).

Summary of actions:
- The feature branch 'feature/MYFEATURE' was merged into 'develop'
- Feature branch 'feature/MYFEATURE' has been removed
- You are now on branch 'develop'

 jake.ko  ~/Dev/git-flow-test   develop  ll
total 8
drwxr-xr-x  25 jake.ko  staff  800  2  7 18:01 ..
drwxr-xr-x   4 jake.ko  staff  128  2  7 20:46 .
-rw-r--r--   1 jake.ko  staff   11  2  7 20:46 myfeature.txt
drwxr-xr-x  14 jake.ko  staff  448  2  7 20:47 .git
```

## 기능을 게시(publish)
```bash
 ✘ jake.ko  ~/Dev/git-flow-test   develop  git flow feature publish MYFEATURE
```

## 게시된 기능 가져오기
```bash
 ✘ jake.ko  ~/Dev/git-flow-test   develop  git flow feature pull origin MYFEATURE
```

## 릴리즈 시작
```bash
 ✘ jake.ko  ~/Dev/git-flow-test   develop  git flow release start RELEASE
Switched to a new branch 'release/RELEASE'

Summary of actions:
- A new branch 'release/RELEASE' was created, based on 'develop'
- You are now on branch 'release/RELEASE'

Follow-up actions:
- Bump the version number now!
- Start committing last-minute fixes in preparing your release
- When done, run:

     git flow release finish 'RELEASE'

 jake.ko  ~/Dev/git-flow-test   release/RELEASE  git flow release publish RELEASE
Counting objects: 3, done.
Writing objects: 100% (3/3), 254 bytes | 254.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'release/RELEASE' on GitHub by visiting:
remote:      https://github.com/kjs850/git-flow-test/pull/new/release/RELEASE
remote:
To https://github.com/kjs850/git-flow-test.git
 * [new branch]      release/RELEASE -> release/RELEASE
Already on 'release/RELEASE'
Your branch is up to date with 'origin/release/RELEASE'.

Summary of actions:
- A new remote branch 'release/RELEASE' was created
- The local branch 'release/RELEASE' was configured to track the remote branch
- You are now on branch 'release/RELEASE'

```

## 릴리스 완료
```bash
jake.ko  ~/Dev/git-flow-test   release/RELEASE  git flow release finish RELEASE
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
Merge made by the 'recursive' strategy.
 myfeature.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 myfeature.txt
Deleted branch release/RELEASE (was 102c09d).

Summary of actions:
- Latest objects have been fetched from 'origin'
- Release branch has been merged into 'master'
- The release was tagged 'RELEASE'
- Release branch has been back-merged into 'develop'
- Release branch 'release/RELEASE' has been deleted
```


## 핫픽스 시작
```bash
jake.ko  ~/Dev/git-flow-test   master  git flow hotfix start hotfix-1
Switched to a new branch 'hotfix/hotfix-1'

Summary of actions:
- A new branch 'hotfix/hotfix-1' was created, based on 'master'
- You are now on branch 'hotfix/hotfix-1'

Follow-up actions:
- Bump the version number now!
- Start committing your hot fixes
- When done, run:

     git flow hotfix finish 'hotfix-1'
```

## 핫픽스 완료
```bash
jake.ko  ~/Dev/git-flow-test   hotfix/hotfix-1  git flow hotfix finish hotfix-1
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
Merge made by the 'recursive' strategy.
 something.txt | 1 +
 1 file changed, 1 insertion(+)
Switched to branch 'develop'
Merge made by the 'recursive' strategy.
 something.txt | 1 +
 1 file changed, 1 insertion(+)
Deleted branch hotfix/hotfix-1 (was b4e2485).

Summary of actions:
- Latest objects have been fetched from 'origin'
- Hotfix branch has been merged into 'master'
- The hotfix was tagged 'hotfix-1'
- Hotfix branch has been back-merged into 'develop'
- Hotfix branch 'hotfix/hotfix-1' has been deleted

 jake.ko  ~/Dev/git-flow-test   develop  git status
On branch develop
nothing to commit, working tree clean
 jake.ko  ~/Dev/git-flow-test   develop  git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
 jake.ko  ~/Dev/git-flow-test   master  git push && git push --tags
Counting objects: 4, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 362 bytes | 362.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To https://github.com/kjs850/git-flow-test.git
   47ce058..3963404  master -> master
Counting objects: 1, done.
Writing objects: 100% (1/1), 157 bytes | 157.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To https://github.com/kjs850/git-flow-test.git
 * [new tag]         hotfix-1 -> hotfix-1
 jake.ko  ~/Dev/git-flow-test   master 
```



## reference
[cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html)

tags:
