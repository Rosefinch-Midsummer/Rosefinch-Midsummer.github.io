---
title: "AI编程工具指北"
date: 2025-04-30T21:29:25+08:00
lastmod: 2025-04-30T21:29:22+08:00
math: true
categories:
- 计算机
- 编程
tags:
- AI
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

## 前言

虽然我平时最常用的是字节跳动出品的Trae，但在某种意义上，我也是最早使用Cursor的用户之一。

待我有空的时候，就打算开发一个基于Trae的Custom Agents Rules Generator，模拟类似的AI编程体验。

## Trae近期发展

Trae近期也在推出一些令人期待的升级：

- **@Agent**：将Trae转变为一个多才多艺、随时待命的AI专家团队。
- **MCP（Universal Communication Framework）**：实现不同AI能力之间的无缝协作。
- **AI规则**：可以定制符合你工作流程的专属智能助手。
- **增强的Context功能**：扩展的#Context能力，为你的项目提供更稳固的知识基础。

### 规则类型概述

Trae IDE支持多种规则类型，主要包括：

|规则类型|说明|
|---|---|
|个人规则|基于用户偏好和需求为AI量身定制，确保输出更贴合个人风格。例如：偏好简洁、严谨或幽默的表达；操作系统适配（Windows/macOS）；内容深度（是否需要详尽解释或只需结论）；交互方式（直接回答或引导提问）。这些规则在所有项目中均生效，帮助个性化AI体验。|
|项目规则|针对特定项目设定的规则，仅在对应项目中生效。例如：代码风格（缩进、命名规范）、所用编程语言（Python、JavaScript等）、框架选择（React、Django等）或API限制，确保AI输出符合项目需求，提升开发效率。|

## Cursor Custom Agents Rules Generator

[cursor-custom-agents-rules-generator](https://github.com/bmadcode/cursor-custom-agents-rules-generator)

## 如何高效使用编程辅助工具 Cursor？

作者：带上幻想的笔  
链接：[https://www.zhihu.com/question/1339583068/answer/1889536971539452217](https://www.zhihu.com/question/1339583068/answer/1889536971539452217)  
来源：知乎  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

---

### 1. 不要急着写代码，先做好整体规划

很多开发者一打开 [Cursor](https://zhida.zhihu.com/search?content_id=720455281&content_type=Answer&match_order=1&q=Cursor&zhida_source=entity)（一种基于人工智能技术的编程辅助工具）或者其他 AI 编程工具时，就直接开始随意提出需求，盲目写代码。这导致代码质量不高、问题频出。

正确的做法是，先在项目中准备好一个专用的文件夹，里面要包含完整的规划资料，例如：

- **产品需求文档（PRD, Product Requirement Document，产品需求说明书）**
- **技术栈（Tech Stack，项目所采用的编程语言、框架及相关技术）概览**
- 建议采用的**文件结构**说明
- **前后端开发规范**（代码风格、接口约定等规范）
- `.cursorrules` 配置文件（用于定义 Cursor 工具的项目规则）

使用 Markdown 格式编写并保存这些资料到代码仓库（repo，repository，代码版本管理库）中，方便后续团队协作和工具访问。良好的规划是提高 AI 编程工具效果的首要前提。

---

### 2. 不要从零开始构建——充分利用已有基础

Cursor 这类 AI 工具在已有代码基础上效果更佳。建议先利用诸如 V0、Lovable 或 Bolt这类工具，快速生成可用的功能界面（functional screens）。

把握快速构建最小可行产品（**MVP, Minimum Viable Product，最小可行性产品**）80%的基本功能，再将基础代码导入 Cursor，利用其强大的 AI 功能优化代码结构、添加业务逻辑，使整个开发过程更高效，质量也更有保证。

---

### 3. 利用“项目规则”（Project Rules）功能规范代码风格与输出

不要再单纯依赖 `.cursorrules` 文件，Cursor 提供“项目规则”（Project Rules）功能，它允许你：

- 针对不同文件类型（例如结构化查询语言 SQL 与 JavaScript）应用不同规则
- 控制 AI 输出时的语气和代码结构格式
- 通过 GitHub（大型代码托管平台）将规则同步给团队成员，实现一致性

通过这些规则设置，Cursor 能像一个根据你团队和项目技术栈量身定制、持续学习的 AI 开发者，极大提升代码生成的适配度和实用性。

---

### 4. 关联技术文档，提高建议和代码的准确度

开启 Cursor 的 @Docs 功能，点击“添加新文档”（Add new doc），同步项目中使用的核心技术文档库，比如：

- Next.js（基于 React 的高性能前端框架）
- Supabase（开源后端即服务平台，与数据库直接交互）
- Stripe（在线支付平台）

这些技术文档为 Cursor 提供详细背景信息（context），使其更准确理解项目需求，生成更高质量且贴合实际的代码和建议。

---

### 5. 使用 @Codebase 功能轻松查询全项目代码库

遇到 Bug 或需快速定位代码时，用 Cursor 的 @Codebase 功能进行提问，如：

- “支付流程是在哪里实现的？”
- “哪个组件负责渲染仪表盘（dashboard）？”

Cursor 会完整扫描项目代码库，结合上下文信息（context），快速定位目标代码或模块，极大节省开发者排查和理解代码的时间。

---

### 6. 配置 MCP（模型上下文协议 Model Context Protocol）实现数据库 Schema 实时访问与自动化

模型上下文协议（Model Context Protocol，MCP）是 Cursor 的一项核心技术，它允许 AI 工具实时读取你在 Supabase 上的数据库 Schema（模式结构）。

有了 MCP，Cursor 可以：

- 动态获取数据库中的数据表（tables）结构
- 自动化编辑数据库 Schema
- 免去手动编写数据库迁移（migration，数据库结构变更管理）文件的繁琐

这使得数据库对 AI 变得可读（machine-readable），极大提升开发效率，被认为是颠覆性的游戏规则改变者（Game changer）。除此之外，MCP 还支持多种高级应用场景。

---

### 7. 利用 AI 自动生成行级安全策略（RLS, Row-Level Security）

行级安全策略（Row-Level Security, RLS）通常被开发者忽视，因为配置复杂。Cursor 通过 AI 自动生成 RLS 策略：

只需简单告诉 Cursor：

“帮我生成 RLS 策略，确保用户只能访问自己的数据。”

它就能在几秒钟内完成准确的安全访问控制规则编写，帮助项目显著提升数据安全性，简化安全管理。

---

### 8. 启用 YOLO 模式（You Only Live Once，即时执行模式）以提升执行速度

默认情况下，Cursor 在执行命令前会先征求用户确认，这样虽安全但拖慢效率。启用 YOLO 模式后：

- 命令会立即执行
- 无需任何确认提示
- 适合熟练且信赖流程的高级用户使用

合理使用 YOLO 模式，可以大幅节省开发流程中的等待和交互时间。

---

### 9. 用截图输入帮助改进用户界面设计

感觉用户界面设计不理想或不够直观？用截图直接拖入 Cursor 界面，或点击聊天窗口下方的图像图标上传屏幕截图，再输入类似：

“请帮我让这个 UI 更简洁、更现代。”

视觉信息的直接输入为 AI 提供额外语境，能实现更高效、更具针对性的 UI 迭代和优化。

---

### 10. 保存并整理优质代码片段，建立个人 AI 开发知识库

每当 Cursor 生成了有价值的代码段或解决方案时：

- 立即保存为 `.md` （Markdown）格式文件，方便日后快速检索和复用
- 将代码片段同时存储在便捷的记事本中，形成个人代码片段库

逐步积累这些优质文本与代码资源，便于打造属于自己的 AI 助手库，让未来开发更加得心应手。

---

### 结语

将 Cursor 视为你可靠的团队伙伴，而非魔术师。只要合理引导和利用它，它能比大多数初级开发者更快速、精准地完成交付任务。











