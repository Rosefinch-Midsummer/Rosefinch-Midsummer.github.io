---
title: "Coursera视频无法播放解决方案"
date: 2024-02-26T18:34:25+08:00
lastmod: 2024-02-26T22:54:22+08:00
math: true
categories:
- 在线课程
tags:
- Coursera
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


# Coursera视频无法播放解决方案

[参考来源](https://zhuanlan.zhihu.com/p/346418260)

## **一、查找ip地址**

**步骤1**：打开 https://www.ipaddress.com/ 这个网站

**步骤2**：解析 d3c33hcgiwev3.cloudfront.net 这个域名

![](https://pic1.zhimg.com/80/v2-a6d357c9e5a31b55a71e7dcb070ea224_1440w.webp)

2024-02-26更新，对于的ip地址如下：

108.156.171.13 d3c33hcgiwev3.cloudfront.net

108.156.171.86 d3c33hcgiwev3.cloudfront.net

108.156.171.132 d3c33hcgiwev3.cloudfront.net

108.156.171.204 d3c33hcgiwev3.cloudfront.net
## **二、修改Hosts**

**步骤3**：找到文件

Windows系统的hosts文件位置：`C:\Windows\system32\drivers\etc`

**步骤4**：把hosts文件复制到桌面并对该文件进行编辑，编辑内容如下⬇️

```text
108.156.171.13 d3c33hcgiwev3.cloudfront.net
108.156.171.86 d3c33hcgiwev3.cloudfront.net
108.156.171.132 d3c33hcgiwev3.cloudfront.net
108.156.171.204 d3c33hcgiwev3.cloudfront.net
```


**步骤五**：把文件拖回原来文件夹，替换原来的hosts。重新刷新网页就行了

必要时也可以按住win+R，弹出运行窗口，输入'cmd'，按'确定'按钮，如下图1所示；输入'ipconfig/flushdns'，显示已成功刷新DNS，就OK啦！

## 附录：win10和win11如何用管理员身份打开hosts文件

[win10和win11如何用管理员身份打开hosts文件](https://blog.csdn.net/m0_37865510/article/details/133700042)

1.在右下角输入框输入cmd，选择“命令提示符（以管理员身份运行）”；

2.在命令行窗口中输入“cd c:/Windows/System32/drivers/etc”

3.输入“notepad hosts”

随后便可以打开hosts文件并对其进行修改和保存。












