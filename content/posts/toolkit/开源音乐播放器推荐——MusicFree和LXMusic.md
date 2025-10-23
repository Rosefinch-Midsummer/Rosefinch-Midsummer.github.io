---
title: "开源音乐播放器推荐——MusicFree和LxMusic"
date: 2025-05-24T23:34:25+08:00
lastmod: 2025-05-24T23:54:22+08:00
math: true
categories:
- 豫游之乐
tags:
- 音乐
- PNPM
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

# 发现你的专属音乐空间：Deep定制的开源音乐播放器——MusicFree

在日益繁忙的生活中，音乐成为许多人不可或缺的精神伴侣。想要一款既自由又灵活的音乐播放器？推荐你试试**MusicFree**——一款开源、免费、极具可定制的本地音乐播放器，特别适合喜欢DIY、追求隐私和高自由度的音乐爱好者。

---

## 🎵 什么是MusicFree？

MusicFree是一款基于插件机制设计的音乐播放器。它的最大亮点在于**插件化架构**：本身不自带任何音源，只是一个纯粹的播放平台，所有的搜索、歌单导入、歌词获取等功能，都是通过插件扩展实现的。这意味着——只要有对应的插件，任何支持的音乐源，都可以被接入。

同时，MusicFree秉持**免费、开源、无广告**原则，支持丰富的自定义界面（浅色/深色模式、自定义背景），在隐私保护方面也做得很好：所有数据都存储在本地，不收集用户信息。

---

## 🔧 配置指南

### 安卓版配置

1. 打开MusicFree应用
2. 点击左上角按钮（菜单）
3. 选择【插件设置】
4. 点击右下角的“+”按钮
5. 选择【从网络安装插件】
6. 输入插件的URL（以`.json`或`.js`结尾），确认安装即可

### PC版配置

1. 打开MusicFree
2. 在左侧菜单中找到【插件管理】
3. 点击顶部的【从网络安装】
4. 输入插件URL（以 `.json` 或 `.js` 结尾）
5. 完成安装后，插件的功能就会被加载到播放器中

**提示：**  
插件链接可以从[MusicFree插件列表](https://musicfree.catcat.work/usage/mobile/install-plugin.html)或者作者官方GitHub获取，支持自己开发或使用第三方插件。

---

## 🚀 快速下载安装

- 官方下载：  
    [MusicFree 官方网站](https://musicfree.catcat.work/)
    
- Github项目：  
    [maotoumao/MusicFree](https://github.com/maotoumao/MusicFree)
    

这里可以找到源代码，随时自定义或参与开发。

---

## 🌟 核心特色

### 插件化设计

- **没有自带音源**，所有搜索/播放/导入功能均通过插件实现
- **多源支持**：只要有插件，任何音乐平台都可以接入，包括国内外主流、私有云等。
- **插件开发简便**：开发者只需定义搜索、播放等标准函数，分页、缓存交由软件管理
- **丰富扩展**：插件市场不断扩充，让你轻松体验新源

### 极致自定义

- 支持浅色/深色模式、背景自定义
- 贴心的用户界面，满足个性化需求

### 隐私优先

- **所有数据存储在本地**，不上传任何个人信息
- 风险控制：使用第三方插件请自行鉴别安全性

### 特殊功能

- **歌词关联**：可以将多首歌的歌词关联起来，实现同步显示，提升听歌体验
- **导入歌单、查看作者、查看专辑**等丰富功能，一站式满足需求

---

## 🧩 使用插件，玩转无限可能

只需几步：

- 在“插件设置”中【从网络安装】输入插件链接（比如GitHub的raw文件地址）
- 或者，安装本地插件
- 完成后即可在播放器中调用不同音源、搜索功能

【官方插件仓库】持续更新，支持多平台多源玩法！

---

## 📢 结语

MusicFree将“播放器”做成了一个**插件的舞台**，供你自由发挥探索。无论你是技术宅，还是单纯希望一款没有广告、纯粹的音乐体验工具，MusicFree都值得一试。

想了解更详细的配置和插件开发指南？请访问  
[官方介绍与文档链接](https://musicfree.catcat.work/plugin/introduction.html)，开启你的定制音乐之旅！

# LX Music

## 关于LX Music

LX Music是一款老牌的桌面音乐软件，支持多平台（Windows、macOS、Linux），以其简洁、实用而著称。虽然早期支持直接在线播放，但目前的版本主要以导入本地音源为核心。这意味着，软件本身不自带音乐库，而是依赖用户自己导入各种音源文件或在线源实现音乐播放。

---

## 数据存储位置

根据不同系统，LX Music的配置和数据存储在不同目录下：

- **Linux：** `$XDG_CONFIG_HOME/lx-music-desktop` 或 `~/.config/lx-music-desktop`
- **macOS：** `~/Library/Application Support/lx-music-desktop`
- **Windows：** `%APPDATA%\lx-music-desktop`

如果你在Windows平台上，且程序文件夹中存在**`portable`**文件夹，那么软件会自动使用此文件夹作为数据存储路径（适用于v1.17.0及以上版本），无需担心配置问题。

---

## 音源资源——动态更新的挑战

**LX Music**的一个特点是需要用户自己导入“音源”或“直播源”。这些音源类似于“直播源”，具有时效性，经常变化或失效，怎么办？

**提醒：**  
不同音源平台的有效性无法保证，建议多测试几个源，选择自己喜欢的。官方提供的音源资源具有一定的时效性，需不断更新。

---

## 在线音源介绍

LX Music支持多种在线音源，主要通过加载外部JavaScript脚本实现。以下是一些官方推荐的在线音源链接（建议复制粘贴使用）：

| 音源名称    | 链接（原始）                                                                                                                                                         | 链接（加速版）                                                                                                                                                                                                                                          |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SixYin  | [https://raw.githubusercontent.com/pdone/lx-music-source/main/sixyin/latest.js](https://raw.githubusercontent.com/pdone/lx-music-source/main/sixyin/latest.js) | [ghproxy](https://ghproxy.net/)加速，如：  <br>[https://ghproxy.net/https://raw.githubusercontent.com/pdone/lx-music-source/main/sixyin/latest.js](https://ghproxy.net/https://raw.githubusercontent.com/pdone/lx-music-source/main/sixyin/latest.js) |
| Huibq   | [https://raw.githubusercontent.com/pdone/lx-music-source/main/huibq/latest.js](https://raw.githubusercontent.com/pdone/lx-music-source/main/huibq/latest.js)   | 同上加速                                                                                                                                                                                                                                             |
| Huibq   | [https://raw.niuma666bet.buzz/Huibq/keep-alive/master/render_api.js](https://raw.niuma666bet.buzz/Huibq/keep-alive/master/render_api.js)                       | 同上加速                                                                                                                                                                                                                                             |
| Flower  | [https://raw.githubusercontent.com/pdone/lx-music-source/main/flower/latest.js](https://raw.githubusercontent.com/pdone/lx-music-source/main/flower/latest.js) | 同上加速                                                                                                                                                                                                                                             |
| Grass   | [https://tt.tenmeng.com/moonue/js/yecao202412.js](https://tt.tenmeng.com/moonue/js/yecao202412.js)                                                             | 同上加速                                                                                                                                                                                                                                             |
| 音乐下载器v5 | [https://api.v2.sukimon.me:19742/script?key=LXMusic_dmsowplaeq](https://api.v2.sukimon.me:19742/script?key=LXMusic_dmsowplaeq)                                 | 无加速链接                                                                                                                                                                                                                                            |

**如果访问GitHub受限，建议用加速链接。这些脚本负责提供不同平台的音乐资源，可根据个人需求选择使用。**

---

## 如何导入在线音源（桌面端）？

操作步骤如下（配图参考）：

1. 打开 **LX Music** 软件，进入【设置】 → 【基本设置】 → 【音乐源】 → 【自定义源管理】
2. 点击【在线导入】，粘贴你所需音源的链接（例如上述在线源链接）
3. 点击【导入】，等待加载完成后，选择刚导入的音源即可使用

## 本地音源导入（尤其适合网络访问缓慢的用户）

如果网络环境不佳，访问GitHub源比较慢，可以提前下载音源脚本到本地，然后通过【自定义源管理】导入本地文件。

---

## 小结

- **LX Music**主要依赖用户自己导入音源或直播源，灵活性高。
- 通过官方推荐的在线源或自定义源，方便不断扩充音乐源。
- 配合多样的导入方式，能满足不同用户的需求。

---

## 温馨提示

- 在线脚本源可能会随时变化，保持定期更新以确保正常播放。
- 网络访问速度有限时，建议多使用本地或缓存源，提升体验。


# [洛雪音乐助手 + 六音自定义音源 v1.2.1](https://www.sixyin.com/8498.html)


---

近年来，五音助手PC版一直紧跟洛雪音乐助手的更新步伐，但随着我工作繁忙，难以持续跟进最新版本。同时，洛雪音乐助手支持自定义音源功能，我便自己编写了一个合用的音源。这样之后，直接使用洛雪的最新版本，再加载自定义的六音音源，就可以享受流畅的听音乐体验。

**注意：由于近期使用人数激增，服务器压力有些大，可能会出现偶尔无法连接的情况，敬请谅解。**

---

## 使用前须知

- **请务必使用最新版的洛雪客户端！**  
    90%以上的问题都是因为版本太旧导致的。
    
- **请勿随意解压文件后再问我怎么用！**  
    我不是售后，遇到问题请详细查阅教程，我也没有收你们的钱。
    
- **国外IP用户请注意：**  
    可能会被服务器拦截，建议不要使用代理上网。
    

为防止恶意滥用，我对接口请求频率做了限制：**3秒内超过5次请求就会封禁IP**。因此，批量下载时可能会频繁失败，原因就是IP被限制。

## 使用指南

1. 下载我提供的自定义音源压缩包，解压得到文件
2. 打开洛雪音乐助手，进入【设置】 — 【音乐来源】 — 【自定义源管理】
3. 点击【导入】，选择解压后的`sixyin-music-resource.js`文件，完成导入
4. 导入成功后，关闭弹窗，将音乐来源切换到“六音音源”
5. 显示“初始化成功”即代表已成功启用，此时就可以使用六音音源听歌

![导入示例图1](https://www.sixyin.com/wp-content/uploads/2024/03/%E6%B4%9B%E9%9B%AA%E9%9F%B3%E4%B9%90%E5%8A%A9%E6%89%8B%E5%85%AD%E9%9F%B3%E8%87%AA%E5%AE%9A%E4%B9%89%E9%9F%B3%E6%BA%90-v1-1-0.png)  
_图1：导入音源文件_

![切换源示意](https://www.sixyin.com/wp-content/uploads/2024/03/%E6%B4%9B%E9%9B%AA%E9%9F%B3%E4%B9%90%E5%8A%A9%E6%89%8B%E5%85%AD%E9%9F%B3%E8%87%AA%E5%AE%9A%E4%B9%89%E9%9F%B3%E6%BA%90-v1-1-0-2.png)  
_图2：切换到六音音源后显示初始化成功_

如果你想了解如何使用自定义Cookie，推荐查看[这里的详细教程](https://www.sixyin.com/10480.html)，视频教程也非常实用。

---

## 关于音乐下载功能

请注意，洛雪默认禁用了下载功能。若想启用，请进入设置，开启下载选项。

![开启下载功能示意图](https://www.sixyin.com/wp-content/uploads/2024/03/%E6%B4%9B%E9%9B%AA%E9%9F%B3%E4%B9%90%E5%8A%A9%E6%89%8B%E5%85%AD%E9%9F%B3%E8%87%AA%E5%AE%9A%E4%B9%89%E9%9F%B3%E6%BA%90-v1-1-0-3.png)

---

## 下载地址

- **洛雪音乐助手电脑版**：[点这里下载](https://www.sixyin.com/114.html)
- **洛雪音乐助手手机版**：[点这里下载](https://www.sixyin.com/7645.html)
- **无损生活（网站提供无损音乐）**： https://flac.life/









