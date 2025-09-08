---
title: "Anki入门教程"
date: 2025-05-17T18:34:25+08:00
lastmod: 2025-05-17T22:54:22+08:00
draft: false
math: true
categories:
- 学习
tags:
- Anki
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

# 如何更好地使用 Anki

## 前言

最近要准备笔试和面试，要记忆好多内容。本来打算自己写一个的特制的Anki软件，但是时间精力显然不够。这个以后再说咯！

Anki 是语言学习、各类考试中不可或缺的强大工具。本文汇总了Anki相关的重要资源，帮助你更好地使用和扩展Anki。

---

## 一、Anki各平台安装包

官网链接（提供最新稳定版本）：  
[https://apps.ankiweb.net/](https://apps.ankiweb.net/)

**备注：**

- 除iOS版本的AnkiMobile是收费软件外，其他平台均免费。
- 医学院学生因考试需大量医学图片，Image Occlusion（图像遮挡）功能使用频繁，极大提升了学习效率。
- 有用户评价：“Medical students are on average about $200,000 in debt, so $x is cheap.”（医学生平均债务约20万美元，花这点钱很划算。）

**Android 版本更新提示：**  
Google Play版本更新较慢，若需最新功能，推荐使用Github上的版本：  
[https://github.com/ankidroid/Anki-Android](https://github.com/ankidroid/Anki-Android)

---

## 二、中文使用手册

官方中文手册，详细介绍Anki的使用方法和功能：  
[https://open-spaced-repetition.github.io/anki-manual-zh-CN/intro.html](https://open-spaced-repetition.github.io/anki-manual-zh-CN/intro.html)

---

## 三、Anki 替代品推荐

虽然Anki功能强大，但以下软件在用户体验和部分功能上也表现优异：

- **氢刻**：[https://qingk.com/](https://qingk.com/)
- **Quizlet**：[https://quizlet.com/](https://quizlet.com/)
- **Supermemo**：[https://www.supermemo.com/](https://www.supermemo.com/)

**个人建议：** 这些替代品虽好，但Anki丰富的插件生态和模板依然难以替代，推荐以Anki为主。

---

## 四、Anki Deck 分享网站

- [https://ankiweb.net/shared/decks](https://ankiweb.net/shared/decks) — 官方共享卡组
- [https://anki-share.com](https://anki-share.com/) — 第三方卡组分享平台
- [https://file.ankichinas.cn/](https://file.ankichinas.cn/) — 中文考试资源（大多数资源收费）

---

## 五、Anki 多端同步方案

- 官方同步在国内速度较慢，有条件建议**自建同步服务器**，提升同步效率。  
    参考教程：[官方同步服务器说明](https://open-spaced-repetition.github.io/anki-manual-zh-CN/sync-server.html)  
    Github项目：[https://github.com/ankitects/anki/tree/main/docs/syncserver](https://github.com/ankitects/anki/tree/main/docs/syncserver)
    
- 若不方便自建服务器，也可通过手动备份恢复`.colpkg`（collection package）实现多端数据同步。  
    详情见：[备份恢复方法](https://open-spaced-repetition.github.io/anki-manual-zh-CN/backups.html)
    

---

## 六、推荐Anki插件

|插件名|功能简介|链接|
|---|---|---|
|Image Occlusion Enhanced|医学生必备的图像遮挡插件|[1374772155](https://ankiweb.net/shared/info/1374772155)|
|AwesomeTTS|文字转语音插件|[1436550454](https://ankiweb.net/shared/info/1436550454)|
|Export to CSV/XLSX|浏览器导出卡片带元数据|[1967530655](https://ankiweb.net/shared/info/1967530655)|
|Export to HTML|导出卡片为HTML格式|[1038895153](https://ankiweb.net/shared/info/1038895153)|
|Batch Editing|批量编辑卡片|[291119185](https://ankiweb.net/shared/info/291119185)|
|Advanced Browser|高级浏览器功能|[874215009](https://ankiweb.net/shared/info/874215009)|
|Enhance Main Window|主窗口增强|[877182321](https://ankiweb.net/shared/info/877182321)|
|Review Heatmap|复习热力图显示|[1771074083](https://ankiweb.net/shared/info/1771074083)|
|Speed Focus Mode|自动提醒、显示及答题模式|[1046608507](https://ankiweb.net/shared/info/1046608507)|
|Add Hyperlink|插入超链接|[318752047](https://ankiweb.net/shared/info/318752047)|
|See Previous Ratings|查看之前卡片评分|[1906641654](https://ankiweb.net/shared/info/1906641654)|
|AnkiConnect|跨程序接口增强|[2055492159](https://ankiweb.net/shared/info/2055492159)|
|Dict2Anki|词典导入卡片|[1284759083](https://ankiweb.net/shared/info/1284759083)|
|Extended Editor for Field|字段扩展编辑器|[805891399](https://ankiweb.net/shared/info/805891399)|
|Quick Colour Changing|快速改变卡片颜色|[2491935955](https://ankiweb.net/shared/info/2491935955)|
|More Overview Stats 2.1|统计数据增强|[738807903](https://ankiweb.net/shared/info/738807903)|

更多插件合集：[https://ankiweb.net/shared/addons](https://ankiweb.net/shared/addons)

---

## 七、Anki模板推荐

以下开源模板项目可帮助你打造美观且功能强大的卡片：

- [ikkz/anki-template](https://github.com/ikkz/anki-template)
- [SweetMeh/Anki-Card-Templates](https://github.com/SweetMeh/Anki-Card-Templates)
- [pranavdeshai/anki-prettify](https://github.com/pranavdeshai/anki-prettify)
- [git9527/anki-awesome-select](https://github.com/git9527/anki-awesome-select)
- [Troyciv/anki](https://github.com/Troyciv/anki)

---

# 附录

## MD2Card

MD2Card 是一个 markdown 转知识卡片工具，可以让你用 Markdown 制作优雅的图文海报。 🌟

![](https://picsum.photos/600/300)

它的主要功能：

1. 将 Markdown 转化为**知识卡片**
2. 多种主题风格任你选择
3. 长文自动拆分，或者根据 markdown `---` 横线拆分
4. 可以复制图片到`剪贴板`，或者下载为`PNG`、`SVG`图片
5. 所见即所得
6. 免费


## Anki Shared Decks 英语学习

[汉译英900句- 汉译音常用表达式经典惯例-陆国强](https://ankiweb.net/shared/info/463461966)

[极品GRE红宝书(简体中文)](https://ankiweb.net/shared/info/2054082259)

[[english] 杨鹏 gre长难句教程](https://ankiweb.net/shared/info/1967691476)
# 参考资料

[Anki 资源汇总](https://zhuanlan.zhihu.com/p/26965799677)







