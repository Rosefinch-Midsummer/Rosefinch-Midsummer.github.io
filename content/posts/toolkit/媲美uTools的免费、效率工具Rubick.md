---
title: "媲美 uTools 的免费、效率工具 Rubick"
date: 2024-01-18T18:34:25+08:00
lastmod: 2024-01-18T22:54:22+08:00
categories:
- 生活
tags:
- 生产力工具
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


# 媲美 uTools 的免费、效率工具 Rubick

[本文来源](https://sspai.com/post/84177)

作者：[muwoo](https://sspai.com/u/sahtlexs/updates)

2023 年 11 月 09 日

> 不知不觉，`Rubick` 从 2021 年开源到现在已经更新到 `v4.x` 版本了，目前整体来看不管是交互形式还是操作便捷性，都达到了一个比较稳定的状态。所以，现在我准备正式的写一篇文章来介绍一下 `Rubick` 了。

## Rubick 是什么？

![](https://cdn.sspai.com/2023/11/06/article/39270428fc2449eea1e93434ad91e9b7?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

rubick 搜索框

`Rubick` 是一款基于 `Electron` 做的开源、免费桌面端效率工具箱；目标是通过一系列辅助插件解决工作、学习、开发上的效率问题。可以把 `Rubick` 理解成一个微信 `App`，插件就是基于微信做的 `小程序`。不过微信的功能主要是 `聊天`；而 `Rubick` 功能主要是 `效率工具`。

> Rubick 名称的灵感来源于一款游戏 `Dota` 。`Rubick（拉比克）` 是 `Dota` 游戏里面的一个英雄名字，这个英雄核心的技能是可以 `**自由使用其他英雄的技能，用完即走**`， 所以觉得非常贴合工具功能的本身，因此得名。

[Rubick github 仓库](https://github.com/rubickCenter/rubick/)

[Rubick 官网](https://rubick.vip/)

[Rubick github 使用手册](https://rubickcenter.github.io/docs/)


## Rubick 有哪些核心功能？

### 1. 搜索系统应用

快捷键 `Alt/Option + R` 在 `Rubick` 搜索框内，输入想要搜索的应用，可以快速检索匹配出相关内容。支持模糊搜索和拼音搜索：

![image.png](https://cdn.sspai.com/2023/11/06/article/d72d3004769869eeb17c59c3ee213935?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

### 2. 安装使用插件

点击 `Rubick` 搜索框最左侧的 logo 图标，可以进入插件市场，选中需要的插件安装后，可以查看到插件的`关键词`（关键词是进行搜索匹配用的）。如需使用插件，只需要在搜索框内输入相关的关键词，即可匹配使用插件。

![QQ20231106-102252-HD (1).gif](https://cdn.sspai.com/2023/11/06/article/06a5ade244ea8c0f1bbb4d1e5f899d86?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

> Rubick 插件是基于 `npm` 的方式进行安装和卸载的。Rubick 内置了 `npm` 包管理器，可以做到在电脑上无 `node & npm` 环境下安装插件。

目前 `Rubick` 中的插件大多是从 `github` 开源的插件中迁移过来的，如果你想自定义开发插件，那么我们也写好了非常清晰的文档来手把手教你如何写一个最基础的 `Rubick` 插件：[插件开发](https://rubickcenter.github.io/docs/dev/)。

如果你开发过 `uTools` 插件，想要把插件迁移到 `Rubick` 也是非常简便的，可以参考这个文档进行插件迁移：[uTools 插件迁移到 rubick](https://github.com/rubickCenter/rubick/issues/105)。

### 3. 基于 WebDav 的数据多端同步

如果你有多个电脑使用了 `Rubick` 并产生了多份数据，这个时候，如果你需要对数据进行多端同步，那么你应该需要用到多端数据同步这个功能。

`Rubick` 多端数据同步功能是基于 `WebDav` 实现的，`Rubick` 本身不会作为中间商来存储用户的任何数据，用户产生的数据将可以直接存储到用户自己的云盘。因此用户数据安全和隐私将会得到极大的保护。

在 `Rubick` 中，使用 `WebDav` 也是非常简便的：`Rubick` 内搜索`偏好设置` 进入 `账户和设置` -> `多端数据同步`；即可对 `rubick` 插件使用数据进行 `导出` 和 `导入`。

![image.png](https://cdn.sspai.com/2023/11/06/article/c1bbafdfc7ebe7f9ca6e64e81146784c?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

目前 `Rubick` 已经内置了 [坚果云](https://www.jianguoyun.com/) 平台的 `webdav` 能力，如果你有坚果云账号，可以直接使用坚果云。如果是其他平台或者自建的 `webdav` 服务，则需要填一下一下服务器地址。

### 4. 便捷的内网部署

做 `Rubick` 的初衷是因为我在公司内部使用 `uTools` 时，需要开发一些个性化插件来满足公司内部的需求，但是插件肯定会产生一些内部数据，这些数据因为安全性是没法发布到 `uTools` 外网的。所以插件一定需要在内网使用。

所以 `Rubick` 解决了这个问题，`Rubick` 所有的插件是基于 `npm` 进行托管的，`Rubick` 提供了让你一键切换源的能力，这样就可以快速便捷的使用内网的插件包，你只需要将你的插件发布到公司 `私有 npm` 源上即可。

![image.png](https://cdn.sspai.com/2023/11/06/article/f1ec15374914b42739af004143adb13e?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

如果你需要了解 `内网部署` 的更多设置，我们也写好了非常详细的文档来帮助你：[内网部署指南](https://rubickcenter.github.io/docs/guide/usage.html#%E5%86%85%E7%BD%91%E9%83%A8%E7%BD%B2)。

### 5. 个性化配置

`Rubick` 主打的就是一个 `开放、自由`。作为自由的代表，个性化界面设置当然少不了：

#### 主界面设置

1. 主题色设置：你可以在 `Rubick` 中自定义主题色，我们提供了 4 套配色方案（立春、立夏、立秋、立冬）供你选择。主题色是我们参考中国风精心选择搭配。
2. 用户信息设置：你可以自定义搜索框 `placeholder` 和 `头像`。

![image.png](https://cdn.sspai.com/2023/11/06/article/f69475865ab19cb823145e276ee46c22?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

#### 基本设置

1. 快捷键设置：你可以设置主程序 `显示/隐藏` 的快捷，和内置 `截图` 功能的快捷键。
2. 暗夜模式和国际化：rubick 支持 `暗夜模式` 和 `中/英文` 切换的国际化设置。

![image.png](https://cdn.sspai.com/2023/11/06/article/f75f4a6cd29ef6132f16f8c7e180bb17?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

#### 本地启动

如果你有很多很多文件和目录，其中有些重要的文件会经常用到，那么你可以把这些文件、文件夹拖入到本地启动栏，这样你就可以在主程序搜索框进行搜索快速启动和搜索到他们：

![QQ20231106-111652-HD (1).gif](https://cdn.sspai.com/2023/11/06/article/9d578e95324ebb75463294abeec7aa84?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

#### 全局快捷键设置

按下快捷键，自动搜索对应关键字，当关键字结果完全匹配，且结果唯一时，会直接指向该功能。示例：

快捷键 「 Alt + W」 关键字 「 微信」

按下Alt + W 直接打开本地微信应用

快捷键 「 Ctrl + Alt + A」 关键字 「 截屏」

按下 Ctrl + Alt + A 进行截屏

## 和商业软件 uTools 的一些区别

### 1. 核心区别

如果你听说过 [uTools](https://u.tools/) ，那你可能会问：这和 `uTools` 有啥区别呢？看着很像啊！ 的确，`rubick` 的开发初衷就是参考 `uTools` 做的。不过，经过我们不懈的努力和迭代，我们已经和 `uTools` 有了大量的差异化：

1. rubick 所有的插件是基于 `npm` 的管理方式，插件发布、安装更加简单、安全。`uTools` 则是需要走他们自己的发布审批流，需要收到打 `upx` 包。
2. rubick 支持 0 成本一键内网部署，而 `uTools` 私有化部署则需要付费。
3. rubick 数据多端同步是基于 `webdav` 做的，所有数据都存储到用户自己的网盘中，没有中间人！！更加安全，而 `uTools` 是他们自己的服务器。
4. rubick 支持系统插件，这对于`todoList`、超级面板`、`超级剪贴板`、`取色器`等插件来说体验是最好的`。`uTools` 不支持。
5. rubick 支持自定义主题、欢迎语、头像... `uTools` 需付费会员。
6. rubick 所有插件都是开源免费、`uTools` 部分热门插件需要二次收费。
7. rubick 所有代码全部开源，可以轻松二开！

### 2. 交互设计上的重构

事情的起因是这样的，刚开始开源的时候，整体的交互和设计大量参考了 `uTools` 主要原因是我是一个独立开发者，没有专门的搞过 `UI` 交互设计这块， 但当我发布 `rubick 1.0` 版本到社区时，收到了大量的质疑，说我是抄袭 `uTools` 的，当时真的是一把辛酸泪。虽说 `UI` 布局上是参考了 `uTools` 可是代码确实我一行一行码出来的 😭。我只是想为大家提供一种社区解决方案而已~

**无奈，我下定决心，有朝一日一定要和** `**uTools**` **在** `**UI**` **上做差异化！**

为了这个心结，前不久，我外包了一个设计师，需要 `￥4000` 块钱来设计改版 `rubick`。 可是作为开源项目，实在是囊中羞涩~，于是我在 `rubick` 交流群里面发起了一个众筹项目：

![](https://cdn.sspai.com/2023/11/06/article/87d71858e9e115eb570c85e473064722?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

本以为会石沉大海，但令我感到意外的是不到 1h 就筹够了 2000+ 的金额。 **这里再次致谢所有参与众筹的小伙伴们！**

为了不辜负小伙伴们的期待，在国庆节前，设计师终于给到我新版的交互设计稿。 `2023 年 10 月` 那个国庆节我自己在家加班加点，终于赶在节后，我们发布了 `rubick v4` 版本，对整体的交互和设计做了大量改动。🎉 🎉

## 最后

开源的路程真的不容易，这里充满了质疑和坎坷，需要的是坚定的信念和那份热爱开源的心！







