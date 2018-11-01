---
title: Git创建本地分支并关联远程分支
date: 2018-10-29 14:16:57
tags:
    - git
---
## 创建本地分支
- git branch 分支名

## 切换到本地分支
- git checkout 分支名

## 创建本地分支并切换到该分支
-  git checkout -b 分支名

## 提交本地分支到远程仓库
- git push origin 本地分支名

## 将新建的本地分支与远程分支关联
-git branch --set-upstream-to=origin/远程分支名  本地分支名
 使用git branch --set-upstream 本地分支名 origin/远程分支名 命令报如下错误
fatal: the '--set-upstream' option is no longer supported. Please use '--track' or '--set-upstream-to' instead.
