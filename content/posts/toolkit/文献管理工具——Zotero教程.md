---
title: "文献管理工具——Zotero教程"
date: 2023-05-26T18:34:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
categories:
- 文献
tags:
- zotero
- 文献管理工具
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

## 简介

[文献管理工具 Zotero 介绍](https://blog.hjroyal.top/posts/tools/2020-09-zotero/)

Zotero是一款自由及开放源代码的文献管理软件，用以管理书目信息及相关材料。其最著名的特性是作为浏览器插件、在线同步、与文档编辑软件如Microsoft Word、LibreOffice、OpenOffice.org Writer、NeoOffice等集成，可生成文内引用、生成页面脚注或文后的参考文献。日常使用中还可以搭配上海交大相关人员维护的[ SJTUThesis LaTeX 模版](https://github.com/sjtug/SJTUThesis)。

## 与其它工具的对比

目前市面上的可选工具有 Mendeley、Endnote、 Papers等，不过这些工具都价格不菲。而Zotero开源免费，比较方便新手开始文献管理之路。再好的软件也只是一个工具，用好用熟练就是最好的。适合自己才是最好的。

## 软件安装 

[官网](https://www.zotero.org/)

按照指引步骤安装即可。然后注册一个 zotero 账号。

需要注意的是，zotero 免费空间只有300MB，需要我们用WebDAV的方式如坚果云来扩充空间。

官网上还有浏览器插件 Zotero Connector 。这个插件可以在打开 zotero 的情况下在浏览器上保存文献条目到软件内。 


## 插件安装

进入 zotero 软件菜单栏中点击工具选择附加组件， 将下载好的.xpi 插件源文件拖放到此窗口 。

很多都是发布在 github 仓库的开源插件，readme 文件有具体功能介绍和使用方法，进入 release 界面就能下载最新版本。

常用插件下载：

- [Better BibTex](https://github.com/retorquere/zotero-better-bibtex) 配合 Latex 文献引用
- [Jasminum](https://github.com/l0o0/jasminum)茉莉花中文支持插件 
- [Zotero PDF Translate](https://github.com/windingwind/zotero-pdf-translate) 翻译插件 
- [ZotFile](http://zotfile.com/) pdf 管理插件 
- [Delitem](https://github.com/redleafnew/delitemwithatt) 删除条目的同时删除附件 
- [Mdnotes](https://github.com/argenos/zotero-mdnotes) 设置模板生成 markdown 笔记框架 
- [Zotero Tag](https://github.com/windingwind/zotero-tag#readme) 标签管理 

更多插件参考[官网插件列表](https://www.zotero.org/support/plugins) 

超有用的zotero笔记：[桃不一的帮助文档 ](https://www.wolai.com/tduPkfFr6iPVkd8UpdmZLJ)

[Zotero 中文社区](https://zotero-chinese.gitee.io/zotero-plugins)

## 常用功能介绍 

### 文献导入 

单个pdf 文件直接拖拽到软件内就能保存到数据库，亦可以用浏览器内 zotero connector 插件保存到软件内。 

### 文献导出 

导出 pdf 附件，按住 ctrl 多次点击，或 ctrl+A 多选，右键可以导出选中所有 pdf 到指定文件夹。 

### 附件管理 

- 设置 zotfile 插件，自定义重命名附件名称，便于查看 pdf 文档。 
- 添加笔记，简要文字可以添加自带笔记附件，作为文献条目的附件。丰富图文的笔记可以借助 mdnotes 插件设置 markdown 模板，然后每一个文件就可以通过模板生成 markdown 笔记框架。配合开源软件 [MarkText](https://github.com/marktext/marktext) 管理，可以无缝生成博客笔记。
- 自定义附件和文献库数据保存位置。【编辑】–【首选项】–【高级】–【文件和文件夹】。通过自定义数据文件夹位置，可以传到网盘将文件夹备份。恢复数据，再放到自定义位置就好。

### 划词翻译 

安装好了翻译插件，在内置 pdf 阅读器界面，点开右边侧栏，就可以实现划词翻译。

## 利用坚果云保存同步文件

[坚果云官网](https://www.jianguoyun.com/)

[# Zotero+坚果云实现文献管理](https://zhuanlan.zhihu.com/p/413147687)

[# 如何在Zotero中设置webdav连接到坚果云？](https://help.jianguoyun.com/?p=3168)

登录后点击右上角用户名旁边的下拉箭头，选择账户信息，点击“安全选项”，添加应用zotero(注意一定要小写！)，这里的应用密码我们后面会用到。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526225241.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526225307.png)


打开zotero然后点击【编辑】再点击【首选项】

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526181749.png)

打开【同步】，**Zotero同步服务器**里登录的是你的Zotero账号和密码，在下面的**文件同步**里选择使用【WebDav】

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526230029.png)

在这里填写你的坚果云的服务器地址：https://dav.jianguoyun.com/dav/，用户名是坚果云账号，密码是一开始设置的应用密码（非坚果云账号登录密码），设置好后选择ok即可。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526230119.png)

回到首页，点击右边的绿色的圈就可以同步更新，如果是第一次设置，会提示在坚果云里自动创建一个名叫：zotero的文件夹，用于存放同步更新的文件。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526230201.png)

**备注**：如果在坚果云里新建了一个文件夹，想将文件放在那个文件夹里的话，那么在填写服务器地址时，需要添加对应的文件夹名字（建议文件夹用英文或数字命名），例如work，那么服务器地址填写如下:

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526230233.png)
如此设置后，就是在work下新建zotero文件夹。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526230320.png)

## 后记

工具虽好，也得常用啊！同步数据后发现多年前读过的论文居然这么多——致敬我曾经荒诞又自负的青春岁月！

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230526181842.png)



