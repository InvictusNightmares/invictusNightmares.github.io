---
layout:     post
title:      "Some commands from Git"
subtitle:   "Git的一些命令"
tags:
   - others
---
# Git的一些命令
最近项目中引入了Git，由于成员较多，在Git的使用中也遇到了一些问题，所以根据项目总结了几个Git命令：
## 查看分支最后一次提交者:
`git for-each-ref --format='%(committerdate) %09 %(authorname) %09 %(refname)' | sort -k5n -k2M -k3n -k4n`
## 查看分支还没合并之前第一次提交者:
`git log --format="%ae %an" master..<HERE_COMES_BRANCH_NAME> | tail -1`
## 创建分支时写入信息:
`git branch --edit-description`
## 查询分支信息:
`git config branch.<branch>.description`
## 快速美观查看分支最后一次提交者：
`git for-each-ref --format='%(color:cyan)%(authordate:format:%m/%d/%Y %I:%M %p)    %(align:25,left)%(color:yellow)%(authorname)%(end) %(color:reset)%(refname:strip=3)' --sort=authordate refs/remotes`

参考[Find out git branch creator](https://stackoverflow.com/questions/12055198/find-out-git-branch-creator/19135644#19135644)
