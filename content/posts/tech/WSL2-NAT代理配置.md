---
title: "WSL2-NAT代理配置"
date: 2025-03-19T18:34:25+08:00
lastmod: 2025-03-19T22:54:22+08:00
draft: false
math: true
categories:
- 计算机
tags:
- WSL2
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


# 使用WSL2时控制台输出“wsl: 检测到 localhost 代理配置，但未镜像到 WSL。NAT 模式下的 WSL 不支持 localhost 代理“

[参考资料](https://blog.csdn.net/weixin_62355896/article/details/134458330)

## 解决方案

**原文在[这里](https://www.cnblogs.com/LLW-NEU/p/17857553.html)**

打开或创建WSL配置文件(位于C:/User/%你的用户名/.wslconfig),并添加以下内容：

```
[experimental]
autoMemoryReclaim=gradual  
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true
```

然后在PowerShell中执行`wsl --shutdown`关闭WSL2，之后再重启WSL2，这个提示就消失了。







