---
title: "Markdown 转海报编辑器系列"
date: 2025-08-07T18:34:25+08:00
lastmod: 2025-08-07T20:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- Markdown
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

# MD2Card：基于Markdown文档生成精美知识卡片

[MD2Card：基于Markdown文档生成精美知识卡片](https://blog.csdn.net/horses/article/details/148693390)

[MD2Card](https://md2card.cn/zh) 是一个免费易用的 Markdown 转知识卡片工具，支持多种精美风格、长文自动拆分、一键导出图片，无论是学习笔记、知识整理还是内容分享，都能轻松搞定。

## 卡片风格

MD2Card 支持温暖柔和、玻璃拟态、简约高级灰、梦幻渐变、波普艺术、赛博朋克、清新自然等 20+ 主题风格。
## Markdown支持

MD2Card 支持标准 Markdown 语法和一些扩展语法，包括标题、列表、代码块、表格、数学公式、流程图、时序图等。同时还可以启用 MDX 语法支持和高级组件。
## 实时转换

MD2Card 采用响应式设计，可以实时预览并快速将 Markdown 文档转换为精美的知识卡片；同时还支持分享和导出功能，导出格式支持 PNG、JPG、SVG、PDF、视频等。

## 公众号排版

MD2Card 提供了公众号排版模式，支持直接复制到公众号文章功能。

## API 调用

高级用户可以使用 MD2Card API 或 MCP Server 生成精美的卡片，MD2Card 官方提供了 Coze 插件，相关功能可能需要消耗积分。

## 在线使用

MD2Card 在线版本可以免费使用，输入以下网址：

https://md2card.cn/zh/editor

# Markdown-to-Image：开源的在线 Markdown 转海报编辑器

[Markdown To Poster](https://github.com/gcui-art/markdown-to-image)

这个 React 组件用于将 Markdown 渲染为漂亮的社交媒体图片。此外，该项目还包括一个内置的 WEB Editor，一键部署后，可以当做 Markdown 转海报图片在线编辑器使用。

[![markdown-to-image banner](https://github.com/gcui-art/markdown-to-image/raw/main/public/banner.jpg)](https://github.com/gcui-art/markdown-to-image/blob/main/public/banner.jpg)

- [English](https://github.com/gcui-art/markdown-to-image/blob/main/README.md) | [中文](https://github.com/gcui-art/markdown-to-image/blob/main/README_CN.md)
- [DEMO & WEB Editor](https://readpo.com/zh/poster)
- [NPM:markdown-to-image](https://www.npmjs.com/package/markdown-to-image)

⭐ 点击 Star 和 Watch 按钮，跟踪我们的最新进展。

## 功能

- [x]  将 Markdown 渲染为适合社交分享的海报图片
- [x]  内置一个模板，支持模板扩展
- [x]  支持自定义主题，并且已内置9个主题
- [x]  支持复制为图像
- [x]  支持一键部署到 Vercel 等
- [x]  已集成图片跨域代理，可以方便的插入在线图片生成图文海报
- [x]  支持复制为HTML 代码，可粘贴到电子邮件和一些编辑器中
- [ ]  更多内置模板

## 如何使用

有两种使用 markdown-to-image 的方式：

- 在项目中集成：markdown-to-image 已导出为一个 React 组件，可以直接集成到您自己的项目中。
- 使用WEB UI：example路径中自带了一个 WEB Editor，部署后，可以当做在线编辑器使用。

### 在你的项目中集成

`markdown-to-image`导出了一个叫 Md2Poster 的组件以及其他三个子组件，你可以通过 npm 等安装使用。

#### 安装

用 npm 安装：

```shell
npm i markdown-to-image
```

用 pnpm 安装：

```shell
pnpm install markdown-to-image
```

用 yarn 安装：

```shell
yarn install markdown-to-image
```

#### 使用

简单开始：

```js
import 'markdown-to-image/dist/style.css'
import { Md2Poster, Md2PosterContent, Md2PosterHeader, Md2PosterFooter } from 'markdown-to-image'

...

const markdown = `
# AI Morning Updates
> On April 29th, what's the latest in the AI field that should be on your radar?
...
`

...

return (

...

<Md2Poster>
  <Md2PosterHeader>Poster Header</Md2PosterHeader>
  <Md2PosterContent>{markdown}</Md2PosterContent>
  <Md2PosterFooter>Powered by ReadPo.com</Md2PosterFooter>
</Md2Poster>

...

)
```

### 使用在线编辑器

#### 使用官方部署的在线编辑器

👉 访问：[ReadPo.com](https://readpo.com/zh/poster)

#### 部署自己的在线编辑器

这里使用Vercel进行部署，点击后一键部署。

# Markdown To Image Serve

一个基于 Next.js 和 Puppeteer 的 Markdown 转图片服务，支持 Docker 部署和 API 集成。A Markdown to Image Service based on Next.js and Puppeteer, supporting Vercel deployment and API integration.

[链接](https://markdown-to-image-plus.vercel.app/)

#### 🚀 基于 Next.js 和 Puppeteer 的 Markdown 转图片服务

将 Markdown 内容高效转换为精美图片，提供开箱即用的 API 接口，支持 Docker 快速部署与二次开发。
## 🎯 项目简介

**Markdown To Image Serve** 是一款开箱即用的 Markdown 转图片 API 服务，基于 Next.js 14 和 Puppeteer 构建，具备以下特性：

### ✨ 核心优势

- 🚀 **一键部署** - 支持 Docker Compose 快速部署
- 🔄 **RESTful API** - 简洁易用的 API 接口
- 🎨 **多主题支持** - 内置 9 种精美主题
- 📱 **响应式设计** - 适配移动端和桌面端
- 🌐 **多平台兼容** - 支持 Docker、Railway、Render 等平台
- 🔒 **安全防护** - 最新安全补丁和防护机制
- ⚡ **性能优化** - 图片压缩、缓存优化

### 🛠️ 技术栈

- **前端**: Next.js 14, React 18, TypeScript
- **UI组件**: Radix UI, Tailwind CSS
- **Markdown**: markdown-to-poster, react-md-editor
- **浏览器**: Puppeteer Core, Chromium
- **部署**: Docker, Railway, Render, Fly.io

---

## 🌟 核心功能

### 📝 内容转换

- Markdown 文本一键转图片
- 支持代码高亮和语法高亮
- 表格渲染和数学公式支持
- 图片和链接处理

### 🎨 样式定制

- **9种内置主题**: blue, pink, purple, green, yellow, gray, red, indigo, SpringGradientWave
- 自定义页眉页脚
- Logo 和品牌元素
- 响应式布局适配

### 🔧 开发工具

- 实时预览编辑器
- 主题切换和参数调整
- 一键复制图片功能
- 批量处理支持

### 📦 API 服务

- RESTful API 接口
- 图片生成和存储
- 错误处理和日志记录
- 健康检查机制

---

### 🌐 在线体验

- [在线服务（Vercel）](https://markdown-to-image-serve.jcommon.top/)
- [GitHub 仓库](https://github.com/wxingheng/markdown-to-image-serve)


# Markdown to Card(Vue)

[jorkun/md2card-v3](https://github.com/jorkun/md2card-v3)

一个纯前端工具，支持将 Markdown 文本实时渲染为美观的卡片，可导出为图片或 .md 文件。

## ✨ 功能

- 实时 Markdown 编辑 + 卡片预览
- 支持 GFM 语法（表格、链接、列表等）
- 一键复制 / 下载 Markdown
- 导出预览图为 PNG
- 无后端，纯前端，部署即用

## 🚀 快速开始

```bash
pnpm install # 或 npm/yarn 
pnpm dev # 启动开发服务器
```

## 📦 打包部署

```bash pnpm build ```

## 🛠️ 技术栈

- Vue 3 + Vite
- Element Plus
- TailwindCSS + @tailwindcss/typography
- html2canvas


# MD2Card(React)

[MD2Card](https://github.com/ittat/md2card)

MD2Card 是一个简洁高效的 Markdown 转换工具，可以将 Markdown 文本转换为精美的卡片图片。

## ✨ 功能特性

- 🚀 实时预览：编辑 Markdown 时即时查看渲染效果
- 🎨 主题切换：内置多种精美主题样式
- 📱 响应式设计：完美适配各种屏幕尺寸
- 💾 自动保存：编辑内容自动保存，无需担心丢失
- 📤 导出图片：一键将卡片导出为图片格式

## 🛠️ 技术栈

- React + TypeScript
- Vite
- Tailwind CSS
- Monaco Editor
- Marked
- Zustand
- Styled Components

## TODO

- ✅ 实现自动分页功能
- ✅ 支持更多 Markdown 语法
- [ ]  实现图片同源加载
- [ ]  优化性能
- [ ]  增加更多主题样式
- [ ]  支持导入导出 Markdown 文件
- [ ]  增加更多导出格式

## 📦 安装

```shell
# 使用 pnpm 安装依赖
pnpm install

# 启动开发服务器
pnpm dev

# 构建生产版本
pnpm build
```

## 🚀 使用方法

1. 在左侧编辑器中输入 Markdown 文本
2. 右侧实时预览渲染效果
3. 使用顶部工具栏调整主题和样式
4. 点击导出按钮保存为图片

## 📸 预览

![项目预览](https://github.com/ittat/md2card/raw/dev/src/assets/image.png)

# MD2Card：基于Markdown文档生成精美知识卡片

[MD2Card：基于Markdown文档生成精美知识卡片](https://blog.csdn.net/horses/article/details/148693390)

[MD2Card](https://md2card.cn/zh) 是一个免费易用的 Markdown 转知识卡片工具，支持多种精美风格、长文自动拆分、一键导出图片，无论是学习笔记、知识整理还是内容分享，都能轻松搞定。

## 卡片风格

MD2Card 支持温暖柔和、玻璃拟态、简约高级灰、梦幻渐变、波普艺术、赛博朋克、清新自然等 20+ 主题风格。
## Markdown支持

MD2Card 支持标准 Markdown 语法和一些扩展语法，包括标题、列表、代码块、表格、数学公式、流程图、时序图等。同时还可以启用 MDX 语法支持和高级组件。
## 实时转换

MD2Card 采用响应式设计，可以实时预览并快速将 Markdown 文档转换为精美的知识卡片；同时还支持分享和导出功能，导出格式支持 PNG、JPG、SVG、PDF、视频等。

## 公众号排版

MD2Card 提供了公众号排版模式，支持直接复制到公众号文章功能。

## API 调用

高级用户可以使用 MD2Card API 或 MCP Server 生成精美的卡片，MD2Card 官方提供了 Coze 插件，相关功能可能需要消耗积分。

## 在线使用

MD2Card 在线版本可以免费使用，输入以下网址：

https://md2card.cn/zh/editor

# Markdown-to-Image：开源的在线 Markdown 转海报编辑器

[Markdown To Poster](https://github.com/gcui-art/markdown-to-image)

这个 React 组件用于将 Markdown 渲染为漂亮的社交媒体图片。此外，该项目还包括一个内置的 WEB Editor，一键部署后，可以当做 Markdown 转海报图片在线编辑器使用。

[![markdown-to-image banner](https://github.com/gcui-art/markdown-to-image/raw/main/public/banner.jpg)](https://github.com/gcui-art/markdown-to-image/blob/main/public/banner.jpg)

- [English](https://github.com/gcui-art/markdown-to-image/blob/main/README.md) | [中文](https://github.com/gcui-art/markdown-to-image/blob/main/README_CN.md)
- [DEMO & WEB Editor](https://readpo.com/zh/poster)
- [NPM:markdown-to-image](https://www.npmjs.com/package/markdown-to-image)

⭐ 点击 Star 和 Watch 按钮，跟踪我们的最新进展。

## 功能

- [x]  将 Markdown 渲染为适合社交分享的海报图片
- [x]  内置一个模板，支持模板扩展
- [x]  支持自定义主题，并且已内置9个主题
- [x]  支持复制为图像
- [x]  支持一键部署到 Vercel 等
- [x]  已集成图片跨域代理，可以方便的插入在线图片生成图文海报
- [x]  支持复制为HTML 代码，可粘贴到电子邮件和一些编辑器中
- [ ]  更多内置模板

## 如何使用

有两种使用 markdown-to-image 的方式：

- 在项目中集成：markdown-to-image 已导出为一个 React 组件，可以直接集成到您自己的项目中。
- 使用WEB UI：example路径中自带了一个 WEB Editor，部署后，可以当做在线编辑器使用。

### 在你的项目中集成

`markdown-to-image`导出了一个叫 Md2Poster 的组件以及其他三个子组件，你可以通过 npm 等安装使用。

#### 安装

用 npm 安装：

```shell
npm i markdown-to-image
```

用 pnpm 安装：

```shell
pnpm install markdown-to-image
```

用 yarn 安装：

```shell
yarn install markdown-to-image
```

#### 使用

简单开始：

```js
import 'markdown-to-image/dist/style.css'
import { Md2Poster, Md2PosterContent, Md2PosterHeader, Md2PosterFooter } from 'markdown-to-image'

...

const markdown = `
# AI Morning Updates
> On April 29th, what's the latest in the AI field that should be on your radar?
...
`

...

return (

...

<Md2Poster>
  <Md2PosterHeader>Poster Header</Md2PosterHeader>
  <Md2PosterContent>{markdown}</Md2PosterContent>
  <Md2PosterFooter>Powered by ReadPo.com</Md2PosterFooter>
</Md2Poster>

...

)
```

### 使用在线编辑器

#### 使用官方部署的在线编辑器

👉 访问：[ReadPo.com](https://readpo.com/zh/poster)

#### 部署自己的在线编辑器

这里使用Vercel进行部署，点击后一键部署。

# Markdown To Image Serve

一个基于 Next.js 和 Puppeteer 的 Markdown 转图片服务，支持 Docker 部署和 API 集成。A Markdown to Image Service based on Next.js and Puppeteer, supporting Vercel deployment and API integration.

[链接](https://markdown-to-image-plus.vercel.app)

#### 🚀 基于 Next.js 和 Puppeteer 的 Markdown 转图片服务

将 Markdown 内容高效转换为精美图片，提供开箱即用的 API 接口，支持 Docker 快速部署与二次开发。
## 🎯 项目简介

**Markdown To Image Serve** 是一款开箱即用的 Markdown 转图片 API 服务，基于 Next.js 14 和 Puppeteer 构建，具备以下特性：

### ✨ 核心优势

- 🚀 **一键部署** - 支持 Docker Compose 快速部署
- 🔄 **RESTful API** - 简洁易用的 API 接口
- 🎨 **多主题支持** - 内置 9 种精美主题
- 📱 **响应式设计** - 适配移动端和桌面端
- 🌐 **多平台兼容** - 支持 Docker、Railway、Render 等平台
- 🔒 **安全防护** - 最新安全补丁和防护机制
- ⚡ **性能优化** - 图片压缩、缓存优化

### 🛠️ 技术栈

- **前端**: Next.js 14, React 18, TypeScript
- **UI组件**: Radix UI, Tailwind CSS
- **Markdown**: markdown-to-poster, react-md-editor
- **浏览器**: Puppeteer Core, Chromium
- **部署**: Docker, Railway, Render, Fly.io

---

## 🌟 核心功能

### 📝 内容转换

- Markdown 文本一键转图片
- 支持代码高亮和语法高亮
- 表格渲染和数学公式支持
- 图片和链接处理

### 🎨 样式定制

- **9种内置主题**: blue, pink, purple, green, yellow, gray, red, indigo, SpringGradientWave
- 自定义页眉页脚
- Logo 和品牌元素
- 响应式布局适配

### 🔧 开发工具

- 实时预览编辑器
- 主题切换和参数调整
- 一键复制图片功能
- 批量处理支持

### 📦 API 服务

- RESTful API 接口
- 图片生成和存储
- 错误处理和日志记录
- 健康检查机制

---

### 🌐 在线体验

- [在线服务（Vercel）](https://markdown-to-image-serve.jcommon.top/)
- [GitHub 仓库](https://github.com/wxingheng/markdown-to-image-serve)


# Markdown to Card(Vue)

[jorkun/md2card-v3](https://github.com/jorkun/md2card-v3)

一个纯前端工具，支持将 Markdown 文本实时渲染为美观的卡片，可导出为图片或 .md 文件。

## ✨ 功能

- 实时 Markdown 编辑 + 卡片预览
- 支持 GFM 语法（表格、链接、列表等）
- 一键复制 / 下载 Markdown
- 导出预览图为 PNG
- 无后端，纯前端，部署即用

## 🚀 快速开始

```bash
pnpm install # 或 npm/yarn 
pnpm dev # 启动开发服务器
```

## 📦 打包部署

```bash pnpm build ```

## 🛠️ 技术栈

- Vue 3 + Vite
- Element Plus
- TailwindCSS + @tailwindcss/typography
- html2canvas


# MD2Card(React)

[MD2Card](https://github.com/ittat/md2card)

MD2Card 是一个简洁高效的 Markdown 转换工具，可以将 Markdown 文本转换为精美的卡片图片。

## ✨ 功能特性

- 🚀 实时预览：编辑 Markdown 时即时查看渲染效果
- 🎨 主题切换：内置多种精美主题样式
- 📱 响应式设计：完美适配各种屏幕尺寸
- 💾 自动保存：编辑内容自动保存，无需担心丢失
- 📤 导出图片：一键将卡片导出为图片格式

## 🛠️ 技术栈

- React + TypeScript
- Vite
- Tailwind CSS
- Monaco Editor
- Marked
- Zustand
- Styled Components

## TODO

- ✅ 实现自动分页功能
- ✅ 支持更多 Markdown 语法
- [ ]  实现图片同源加载
- [ ]  优化性能
- [ ]  增加更多主题样式
- [ ]  支持导入导出 Markdown 文件
- [ ]  增加更多导出格式

## 📦 安装

```shell
# 使用 pnpm 安装依赖
pnpm install

# 启动开发服务器
pnpm dev

# 构建生产版本
pnpm build
```

## 🚀 使用方法

1. 在左侧编辑器中输入 Markdown 文本
2. 右侧实时预览渲染效果
3. 使用顶部工具栏调整主题和样式
4. 点击导出按钮保存为图片

## 📸 预览

![项目预览](https://github.com/ittat/md2card/raw/dev/src/assets/image.png)
















