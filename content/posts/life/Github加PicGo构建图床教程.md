---
title: "Github加PicGo构建图床教程"
date: 2023-05-05T23:34:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
categories:
- 博客
tags:
- 图床
- PicGo
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


[参考文章来源](https://www.cnblogs.com/maluyelang/p/17253594.html)

## 在GitHub上创建新仓库

先在Github创建一个新仓库，用于存放图片，仓库必须是public的，否则存储的图片不能正常访问。

## 安装并配置PicGo

[PicGo-github](https://github.com/Molunerfinn/PicGo)

1.  如果尚未安装，安装并打开 PicGo。
    
2.  点击左侧菜单栏上的“图床设置”。
    
3.  在“图床设置”页面，选择“GitHub”作为存储服务。
    
4.  填写配置信息：
    
    **仓库名称（Repository）**：请输入 xxxx/repo_name。  
    **分支名（Branch）**：默认为 main 或 master，您可以在 GitHub 仓库中查看默认分支名称。  
    **访问令牌（Token）**：您需要在 GitHub 上创建一个访问令牌。请参阅以下说明来获取令牌。  
    **存储路径（Path）**：根据您的需求，可以将其设置为 / 或其他路径。例如，设置为 /images/，您上传的图片将存储在仓库的 /images/ 目录下。  
    **自定义域名（Custom Domain）**：此处可选。如果您有自定义域名，可以在此填写，否则请留空。
    
5.  创建访问令牌（Token）：
    
    1.  打开 GitHub，点击右上角的头像，然后选择“Settings”。
    2.  在左侧导航栏中，点击“Developer settings”。
    3.  接着，点击“Personal access tokens”。
    4.  点击右上角的“Generate new token”按钮。
    5.  为令牌命名（例如“PicGo”），然后勾选“repo”权限。
    6.  点击页面底部的“Generate token”按钮。
    7.  复制生成的令牌，然后将其粘贴到 PicGo 配置中的“Token”字段。
    8.  在PicGo 的“GitHub”配置中填写令牌，然后点击“确认修改”。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230505231534.png)

## 设定自定义域名用CDN加速

[jsdelivr官网——# A free CDN for open source projects](https://www.jsdelivr.com/)

可以为空。这里为了使用 CDN 加快图片的访问速度，填写：

`https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01`


```txt
// load any GitHub release, commit, or branch

// note: we recommend using npm for projects that support it

[https://cdn.jsdelivr.net/gh/user/repo@version/file](https://cdn.jsdelivr.net/gh/user/repo@version/file)

  

// load jQuery v3.6.4

[https://cdn.jsdelivr.net/gh/jquery/jquery@3.6.4/dist/jquery.min.js](https://cdn.jsdelivr.net/gh/jquery/jquery@3.6.4/dist/jquery.min.js)

  

// use a version range instead of a specific version

[https://cdn.jsdelivr.net/gh/jquery/jquery@3.6/dist/jquery.min.js](https://cdn.jsdelivr.net/gh/jquery/jquery@3.6/dist/jquery.min.js)

[https://cdn.jsdelivr.net/gh/jquery/jquery@3/dist/jquery.min.js](https://cdn.jsdelivr.net/gh/jquery/jquery@3/dist/jquery.min.js)

  

// omit the version completely to get the latest one

// you should NOT use this in production

[https://cdn.jsdelivr.net/gh/jquery/jquery/dist/jquery.min.js](https://cdn.jsdelivr.net/gh/jquery/jquery/dist/jquery.min.js)

  

// add ".min" to any JS/CSS file to get a minified version

// if one doesn't exist, we'll generate it for you

[https://cdn.jsdelivr.net/gh/jquery/jquery@3.6.4/src/core.min.js](https://cdn.jsdelivr.net/gh/jquery/jquery@3.6.4/src/core.min.js)

  

// add / at the end to get a directory listing

[https://cdn.jsdelivr.net/gh/jquery/jquery/](https://cdn.jsdelivr.net/gh/jquery/jquery/)

```

## 具体使用

推荐使用Snipaste截图工具，更改热键之后截图，复制到剪切板，用PicGo快捷上传中剪切板图片上传方式快速上传图片，不用占用本地存储空间。

把Github Repo作为图床，需要及时更新Github Token。Token失效后就会上传失败。


## 后记

可以把个人博客、obsidian或typora和该图床联结在一起更好地管理自己的文档！



