---
title: Git使用中遇到的问题
date: 2019-02-18 18:47:36
tags:
---
#### Git 放弃本地更改，拉取远端最新代码
```
git fetch --all
git reset --hard origin/master
git pull
```

### Git commit信息写错了，更改commit信息
```
git commit --amend
//执行此命令后，进入Vi编辑模式，第一句为Commit信息，更改保存退出即可
```
