---
title: "基于Cloudflare平台的精品导航网站开源项目"
date: 2025-06-05T18:34:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
math: true
categories:
- 生活
tags:
- 导航网站
- CloudFlare
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

# 基于Cloudflare平台的精品导航网站开源项目

导航网站不仅仅是简单的一组链接集合，它们更像是通向互联网世界各个角落的桥梁。通过清晰的分类、智能的搜索及个性化推荐，导航网站能够极大提升用户的浏览效率和体验。市面上许多导航项目通常需要传统服务器部署，但随着云端无服务器技术的发展，我们可以利用Cloudflare Worker和Pages这类现代平台，快速搭建免运维、极速访问的个人导航站点。

本文将详细介绍三个优秀的开源导航项目，均基于Cloudflare生态，支持轻松部署与自定义，适合广泛用户搭建属于自己的网址导航。

---

## 一、CF-Worker-Dir：一分钟极速部署的Cloudflare Worker导航站

[GitHub项目地址](https://github.com/sleepwood/CF-Worker-Dir)

这款导航项目基于Cloudflare Worker云函数平台，无需传统服务器，轻量级且易上手。只需几分钟即可部署一个功能完善的导航网站。

### 主要特点

- 利用Cloudflare Worker实现无服务器的快速构建
- 自动构建水底陷阱般精妙的网址分类体系
- 极速响应，无需后台维护，节省成本与时间
- 适合对部署效率和简单维护有较高需求的用户

---

## 二、WebNav Hub：基于Cloudflare Pages的可在线编辑导航站

[GitHub项目地址](https://github.com/bbylw/kvp)

WebNav Hub是一个简洁且可高度自定义的网址导航页面，利用Cloudflare Pages进行托管，支持在线编辑和密码保护的管理功能。

### 功能亮点

- 响应式设计：适配手机、平板及桌面
- 分类展示：直观整理网站链接
- 在线添加/编辑链接，无需本地修改
- 编辑功能支持密码保护，保障安全
- 使用Font Awesome图标，美化界面
- 部署简单，访问速度快

### 部署步骤概览

1. 克隆GitHub仓库
2. 在Cloudflare Dashboard创建Pages项目，绑定GitHub仓库
3. 配置KV命名空间（如`LINKS_KV`）
4. 将KV绑定到Pages项目
5. 设置环境变量，包括`EDIT_PASSWORD`（编辑密码）
6. 重新部署应用

完成后，用户即可通过页面右下角进入编辑模式，输入密码后添加或修改导航链接。

### 自定义指南

- 通过修改`index.html`和`styles.css`调整页面布局与样式
- 在函数文件`functions/api/links.js`添加默认链接
- 通过Cloudflare Dashboard的KV管理删除或维护链接数据

---

## 三、拾光集：基于Cloudflare Workers的精品书签导航平台

[项目地址](https://github.com/wangwangit/nav)  
[示例站点](https://nav.wangwangit.com/)

拾光集是一款优雅且功能丰富的书签收藏与分享平台，利用Cloudflare Workers、D1数据库和KV存储构建，提供完善的后台管理与审核机制。

### 核心功能

- 响应式设计，完美适配各种设备
- 按类别清晰组织书签，支持站内搜索
- 用户提交书签申请，管理员审核确保内容质量
- 安全认证与权限控制保护后台
- 批量导入导出书签，管理高效
- 全面后台管理界面，便于维护与扩展

### 快速开始

- 在线体验：[https://nav.wangwangit.com](https://nav.wangwangit.com/)
- 管理后台入口：[https://nav.wangwangit.com/admin](https://nav.wangwangit.com/admin)

### 部署流程

1. 在Cloudflare控制台创建D1数据库和KV命名空间（`NAV_AUTH`）
2. 新建Workers，替换上传项目中的`worker.js`文件代码
3. 绑定数据库与KV至Worker
4. 部署并通过后台添加首批书签，即可访问成品导航站

### 技术栈

- Cloudflare Workers：边缘计算平台
- Cloudflare D1：边缘SQL数据库
- Cloudflare KV：键值存储
- TailwindCSS：现代实用CSS框架

### 项目结构示例

```
nav/
├── worker.js          # 主程序代码
├── schema.sql         # 数据库结构定义
└── README.md          # 说明文档
```

### 自定义开发

- 通过调整`worker.js`内TailwindCSS配置快速修改主题颜色
- 在`worker.js`中统一管理前端渲染、API请求及后台逻辑，方便拓展新功能

---

# 总结

以上三个项目各具特色：

- **CF-Worker-Dir**：极速无服务器部署，轻量级入门选择；
- **WebNav Hub**：支持在线编辑，适合需要灵活维护的个人或小团队；
- **拾光集**：功能完整，适合想实现专业书签管理与分享的平台搭建。

均依托Cloudflare边缘技术，实现了便捷、快速、安全的导航网站构建体验，适合对服务器管理有顾虑的开发者和用户。欢迎根据自身需求选择合适项目，尝试打造专属的高效互联网入口。











