---
title: "Cloudflare-R2对象存储搭建高速免费图床指南"
date: 2025-05-16T18:34:25+08:00
lastmod: 2025-05-16T22:54:22+08:00
math: true
categories:
- 编程
- 计算机
tags:
- CloudFlare
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


# Cloudflare R2对象存储搭建高速免费图床指南


# 前言

最近打算搭建一个图片画廊。之前使用 GitHub 作为图床，但速度较慢。  

这次尝试用 Cloudflare R2 搭建图床，并通过 `picgo-plugin-s3` 插件实现图片上传。

需要注意的是，PicGo 插件有时会安装失败，甚至导致搜索功能无法使用，这时可以尝试手动安装插件。

---

# 方案优势

搭建好图床后，可以直接在博客或个人网站中使用。该方案具有以下明显优势：

1. **免费**：Cloudflare R2 提供了大量免费额度，满足日常使用需求。
2. **稳定可靠**：无需担心服务商跑路或断服问题。
3. **无网络限制**：生成的图片链接在国内外网络均可正常访问。

---

## 1. Cloudflare R2 价格解析

- 官方价格说明：[Cloudflare R2 定价](https://developers.cloudflare.com/r2/pricing/#free-tier)
- 费用计算器：[R2 Calculator](https://r2-calculator.cloudflare.com/)

以下是 Cloudflare R2 免费额度及超额计费情况：

|类型|免费额度|超额收费|
|---|---|---|
|存储|每月 10 GB|$0.015 / GB / 月|
|A 类操作|每月 100 万次请求|$4.5 / 100 万次请求|
|B 类操作|每月 1000 万次请求|$0.36 / 100 万次请求|
|出口流量|全球免费①|不收费|

> **注解①：** 以下方式访问 R2 不产生出口流量费用：
> 
> - 通过 [Workers API](https://developers.cloudflare.com/workers/) 访问
> - 通过兼容 S3 的 API 访问
> - 通过 `r2.dev` 子域名访问

出口流量指的是数据从 R2 存储桶传输至公网的流量，通常云服务商对此进行收费。Cloudflare R2 的特色在于，符合上述访问模式时，出口流量免费。

- 传统云存储（如 AWS S3）在用户读取资源时会产生流量费用；
- Cloudflare R2 利用其全球网络，实现了内部路由，避免用户流量费用，极大降低成本。

---

# 什么是图床？

图床是存储图片的专用空间。你将博客或网站中使用的图片上传至图床后，图床会为每张图片生成一个可访问的链接，之后可以通过这些链接在博客或网站中加载对应图片。

---

## 常见图床方案对比

|方案|优点|缺点|适用场景|
|---|---|---|---|
|公共图床|上手简单、免费，支持外链|流量有限，有跑路风险|轻量图片发布，如文章配图|
|云存储服务|稳定可靠，CDN加速访问|可能收费，配置较复杂|对性能和速度有要求的场景|
|GitHub仓库|免费，支持版本管理|国内访问慢，新手不易上手|技术博客、技术文档|
|自建图床|完全掌控，数据长期保存|需要服务器及技术支持|长期内容创建或稳定性高需求|
|直接嵌入Markdown|图片伴随文档，无需外链|文件变大，加载慢，不适合多图|少量图片的Markdown文档|
|目标平台存储|方便快捷，平台自动处理图片|不跨平台，迁移需重新上传|特定平台（公众号、知乎等）|

---

# 需要提前准备的事项

使用 Cloudflare R2 和 PicGo 搭建免费图床，需提前准备：

1. 一个提前注册好的 Cloudflare 账号，并添加一个付费计划
    - 不必担心扣费，可以选择0元免费计划
2. 一个提前注册好的域名，可以选便宜一些的
    - 域名后缀无所谓，只是作为图片网址使用
    - 如果不想花一年十几块的域名费，也可以去网上找免费的域名使用


# 搭建 R2 图床流程

本文演示如何使用 Cloudflare R2 和 PicGo 搭建免费图床。

## 1. 配置 Cloudflare R2

登录 Cloudflare，左侧菜单选择「R2 对象存储」。该服务提供每月 10GB 免费存储空间，个人使用已足够。超出部分按约 0.1 元/GB 计费，价格非常优惠。

此外，每月允许 100 万次写入和 1000 万次读取操作，满足个人网站需求。

![Cloudflare R2](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/R2%E4%BB%8B%E7%BB%8D.png)

点击“将 R2 订阅添加到我的账户”，进入存储桶创建页面。自定义存储桶名称，选择靠近主要访问用户的地区，例如针对亚洲可选亚太区，其他保持默认，点击创建完成。

![存储桶](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E5%88%9B%E5%BB%BA%E5%AD%98%E5%82%A8%E6%A1%B6.png)

默认情况下，存储桶无法通过公共 URL 访问。进入对应存储桶的设置，向下找到“R2.dev 子域配置”，点击“允许访问”，输入 `allow` 确认。生效后即可公网访问。

![上传文件](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E5%AD%98%E5%82%A8%E6%A1%B6%E5%88%9B%E5%BB%BA%E5%AE%8C%E6%88%90.png)

回到存储桶对象页，拖入图片上传。

![上传成功](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E4%B8%8A%E4%BC%A0%E5%9B%BE%E7%89%87.png)

上传后点击图片，即可获得 Cloudflare R2 生成的图片访问链接。

![图片网址](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E5%9B%BE%E7%89%87%E7%BD%91%E5%9D%80.png)

将链接复制至浏览器打开，验证图片是否正常显示。Cloudflare R2 支持国内外网络访问。

## 2. 域名托管至 Cloudflare

为了使用自定义域名替换 R2 默认域名，需先将域名托管到 Cloudflare。在左侧点击「网站」，输入自己的域名。

![添加域名](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E5%A1%AB%E5%86%99%E5%9F%9F%E5%90%8D.png)

点击“继续”，选择最下方免费计划，再次点击“继续”，弹窗处确认激活。

![选择免费计划](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E5%85%8D%E8%B4%B9%E8%AE%A1%E5%88%92.png)

向下滑动到“更新名称服务器”，复制生成的两个名称服务器地址。

![生成的网址](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/2%E4%B8%AA%E7%BD%91%E5%9D%80.png)

以阿里云为例，登录控制台，进入域名管理，找到 DNS 设置，修改名称服务器为 Cloudflare 提供的两个地址。

![配置2个网址](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E9%85%8D%E7%BD%AE%E7%BD%91%E5%9D%80.png)

保存配置后，回到 Cloudflare，等待域名状态变为“活动”，表明域名托管成功。

![域名托管成功](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E6%89%98%E7%AE%A1%E6%88%90%E5%8A%9F.png)
## 3. Cloudflare R2 自定义域名

域名托管至 Cloudflare 后，进入所创建的 blog 存储桶，点击右侧“设置”，向下找到“自定义域”，点击“连接域”，输入自定义域名，稍等刷新即可生效。

![实现自定义域](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E8%87%AA%E5%AE%9A%E4%B9%89%E5%9F%9F.png)

打开 blog 存储桶中的图片，会发现除了原始网址外，还生成了一个自定义域名的网址，两者均可访问图片。

![新的图片网址](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/%E6%96%B0%E7%BD%91%E5%9D%80.png)

## 4. PicGo 安装配置

图床搭建完成后，推荐使用开源工具 PicGo 上传图片并获取链接。 [点击下载](https://picgo.github.io/PicGo-Doc/zh/guide/#%E4%B8%8B%E8%BD%BD%E5%AE%89%E8%A3%85)

打开 PicGo，先安装 S3 插件：在插件设置中搜索“S3”，选择安装 s3-lls 插件。若安装失败，重启 PicGo 后重试。

![安装S3插件](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/S3.png)

安装后，进入左侧“图床设置”，选择 Amazon S3 编辑默认配置项。

![S3参数配置](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/picgo%20-%20%E9%85%8D%E7%BD%AE.png)

- 名称：自定义填写即可。
    
- 应用秘钥 ID 和应用秘钥：登录 Cloudflare，进入 R2 对象存储“概述”页，点击“API”→“管理API令牌”→“创建API令牌”，赋予读写对象权限，生成后填写到 PicGo 中。  
    ![生成ID和秘钥](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/ID%E7%A7%98%E9%92%A5.png)
    
- 桶名称填写创建的存储桶名，如 blog。
    
- 文件路径填写 `PicGo/`，上传的文件会统一存放此文件夹下。
    
- 权限保持默认。
    
- 地区填写 `auto`，或存储桶创建时选择的地区。
    
- 自定义节点：同样在 Cloudflare R2“概述”页点击“API”，复制“通过 API 访问 R2 存储”的 HTTPS 地址，粘贴到 PicGo。  
    ![获取子域网址](https://tyxiaoming.top/%E5%9B%BE%E5%BA%8A/API%E7%BD%91%E5%9D%80.png)
    
- 自定义域名填写托管在 Cloudflare 的域名即可。


# PicGo 插件手动安装教程

## 插件picgo-plugin-s3

`picgo-plugin-s3` 是 [PicGo](https://github.com/PicGo/PicGo-Core) 的 Amazon S3 上传插件。

- 支持 Amazon S3 及兼容 S3 API 的云存储服务，如 Backblaze B2
- 支持 PicGo GUI 版本
- 支持 MinIO 服务

安装方式：

- 在 PicGo GUI 中，直接搜索 “S3” 即可安装插件。
- 使用 PicGo Core 版，则在命令行执行：
    
    ```bash
    picgo add s3
    ```
    
    即可完成安装。


## 手动安装插件picgo-plugin-s3

某些情况下，PicGo 插件安装会失败，或者搜索界面无法使用，此时可以选择手动安装插件。

---

### 1. 确认你需要安装的插件

由于插件搜索或自动安装有时会失效，首先需要确认插件的准确名称。  
打开插件仓库：[Plugin for PicGo](https://github.com/PicGo/Awesome-PicGo)，找到你需要的插件。  
例如本文以 `S3` 插件为例，其正式名称为：`picgo-plugin-s3`。

---

### 2. 环境准备

PicGo-core 依赖 Node.js 环境，因此需要在系统中预先安装 Node.js。

> 插件无法正常安装常因环境问题  
> **Node.js 安装方法不再赘述**，可自行搜索安装教程，例如搜索关键词：“nodejs install for windows”。

确认 Node.js 安装成功，可在命令行执行以下命令检查版本：

```bash
node -v
npm -v
```

---

### 3. 安装插件

以 Windows 系统为例，PicGo 的配置文件夹一般位于：

```
C:\Users\{用户名}\AppData\Roaming\picgo
```

> **注意**  
> `AppData\Roaming` 文件夹用于存放应用程序的配置、插件、设置等，非专业用户建议谨慎操作，避免破坏程序正常运行。

在该目录下打开终端（命令行窗口），执行以下命令安装插件：

```bash
npm install picgo-plugin-s3
```

安装完成后，重启 PicGo 即可使用该插件。


# 参考资料

[Cloudflare R2对象存储搭建高速免费图床完全指南](https://zhuanlan.zhihu.com/p/24080167302)

[个人图床最佳方案：Cloudflare R2+PicGo](https://tyxiaoming.xin/2025/01/12/%E6%90%AD%E5%BB%BA%E5%9B%BE%E5%BA%8A/)

[基于CF R2存储的免费图床](https://blog.wangms.org/ops/05_%E5%A6%82%E4%BD%95%E6%90%AD%E5%BB%BA%E4%B8%80%E4%B8%AA%E5%85%8D%E8%B4%B9%E5%9B%BE%E5%BA%8A.html)

[picgo-plugin-s3](https://github.com/wayjam/picgo-plugin-s3)

[PicGo手动安装插件](https://blog.wangms.org/ops/07_PicGo%E6%89%8B%E5%8A%A8%E5%AE%89%E8%A3%85%E6%8F%92%E4%BB%B6.html)



































