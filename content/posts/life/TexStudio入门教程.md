---
title: "TexStudio入门教程"
date: 2023-05-27T18:34:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
categories:
- 格物致知
- Getting Started
tags:
- TexStudio
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

# TexStudio入门教程

[下载地址](https://texstudio.sourceforge.net/)

[TexStudio + MikTex 论文写作环境配置](https://zhuanlan.zhihu.com/p/576955891)

## 简介

TeXstudio 是跨平台的免费软件，是专门用来编辑 `.tex` 文件的工具。

## 安装MikTex

- 安装过程简单
- 宏包自动安装、更新
- 集成保证理，若是需求，软件的集成保证理器会从Internet装载贫乏的组件。例如，LaTeX指令

### 下载

[# Getting MiKTeX](https://miktex.org/download)

### 检查更新

安装完毕之后，检查是否安装成功，`Win + R` 快捷键，输入 `cmd`， 打开命令行，输入`tex -version` ，显示

```text
MiKTeX-TeX 4.5 (MiKTeX 22.10)
© 1982 D. E. Knuth; all rights are reserved.
TeX is a trademark of the American Mathematical Society
using bzip2 version 1.0.8, 13-Jul-2019
compiled with curl version 7.72.0; using libcurl/7.72.0 Schannel
compiled with expat version 2.2.10; using expat_2.2.10
compiled with liblzma version 50020052; using 50020052
compiled with libressl version LibreSSL 3.1.4; using LibreSSL 3.1.4
compiled with MiKTeX Application Framework version 4.6; using 4.6
compiled with MiKTeX Core version 4.16; using 4.16
compiled with MiKTeX Archive Extractor version 4.0; using 4.0
compiled with MiKTeX Package Manager version 4.8; using 4.8
compiled with uriparser version 0.9.4
compiled with zlib version 1.2.11; using 1.2.11
```

安装成功。在“**开始**”中找到“** MikTex Console**”双击打开，出现以下界面，点击“**检查更新**”。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230527202656.png)

然后选择“**更新 -->** **立即更新**”更新宏包

## 安装TeXstudio

[下载地址](https://texstudio.sourceforge.net/)

按照指引安装即可。文件夹路径可以更改，建议和MikTex再同一级目录，便于管理。

### 配置

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230527203213.png)

#### 汉化

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230527203341.png)

#### 修改默认编译器

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230527203425.png)

英文论文写作选择“**PdfLaTeX**”，中文论文选择“**XeLaTex**”。

#### 添加命令

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230527203551.png)

如果没能选择合适的命令，编译时可能报错。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526233846.png)

解决方案：

TeXstudio --> 选项 --> 设置 --> 命令 --> 设置路径，一般路径存在于miktex文件夹下的bin目录下，直接搜索选中即可解决

此外如果自己安装的 MiKTeX 或 CTeX 套装（内部使用 MiKTeX）或 TeX Live 不是所谓完全版，就可能出现在编译时提示你某某文件找不到的情况。这个时候，需要安装宏包。 Windows 下的 MiKTeX 有一个很有用的功能，就是在编译时缺少宏包时，就自动弹出一个对话框，只要点确定，它就联网安装宏包，非常好用。


![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230527000942.png)

点击下面的安装即可自动安装所需宏包

测试成功

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230527001411.png)

## 论文写作

在想要投稿的期刊中找到“**LaTeX模版**”，使用**TexStudio**打开`.tex` 文件，将自己的论文内容放上即可。

`.cls` 文件，是类文件，包含期刊设置好的格式，**勿动、勿修改**；

`.bib` 文件，是参考文献；

`.sty` 文件，是样式文件，即宏包，编译过程中，若是缺失某个宏包，会自动下载。

## 编译运行

![](https://pic3.zhimg.com/80/v2-22cb1f339bfa7e597a6facd7584a386a_1440w.webp)

编译文件，Elsevier单栏模板

## 投稿

成功编译，可以投稿。

若是`.bib`文件或者`.tex`文件进行了修改，PDF中没有变化，需要将临时文件删除，重新编译。

## 更新 TeXstudio

TeXstudio 更新之前需要先卸载旧版。在卸载之前，可以先复制一份用户配置以免配置文件丢失。对于Windows 系统，配置文件一般在 C:\Users\用户名\AppData\Roaming\texstudio 路径下。*nix 系统类似。



