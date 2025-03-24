---
title: "Git 提交代码时一直提交不上去某个文件夹"
date: 2025-03-24T18:34:25+08:00
lastmod: 2025-03-24T22:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- Git
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: ""
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
---


# Git 提交代码时一直提交不上去某个文件夹

[文章来源](https://blog.csdn.net/m0_55051386/article/details/124154771)

## 问题描述

这个文件夹是直接拷贝过去的，在提交到远程仓库是出现了问题。

## 问题分析

直接拷贝过去的文件夹里面有个 .git 的文件，所以在执行 git status 的时候出现 modified: test (modified content, untracked content) 提示，这个提示存在的原因是 xxx目录是一个空目录，且里面有一个.git文件夹。就是因为这个.git文件夹导致这个提示。

## 问题解决

简单操作：`git rm -rf --cached 文件夹名称`

详细操作：把该文件夹里面的 .git 文件删除，然后执行如下命令

```
# 1. 移除错误文件名 test 在git中的进程树

git rm -rf --cached test

# 2. 确认移除

git commit -m '111'

# 3. 提交

git add .
git commit -m '111'
git push origin main
```











