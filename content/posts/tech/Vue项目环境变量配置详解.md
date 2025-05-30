---
title: "Vue 项目环境变量配置详解"
date: 2025-05-30T18:34:25+08:00
lastmod: 2025-05-30T22:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- Vue
- Vite
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

# Vue 项目环境变量配置详解 —— .env、.env.development、.env.production、.env.local 的区别与使用

在 Vue 项目开发中，经常会需要根据不同的环境配置不同的参数，比如接口地址、调试开关等。为了方便管理，Vue 支持通过一系列 `.env` 文件来配置环境变量。本文将详细介绍四种常用 `.env` 文件的区别、优先级、引用方式，以及在实际项目中如何正确配置和使用。

---

## 一、为什么要使用环境变量？

不同环境（开发、测试、生产）接口地址和配置往往不同。如果硬编码在代码里，每次打包上线都需要手动修改，极易出错且不方便维护。通过环境变量，我们可以：

- 根据环境自动切换配置
- 保持代码清洁，避免硬编码
- 支持本地个性化配置，不影响团队其他人

---

## 二、四种 `.env` 文件的区别

|文件名|作用|是否被版本控制|适用场景|
|---|---|---|---|
|`.env`|所有环境通用的默认变量|通常被版本控制|基础配置，所有环境共享|
|`.env.development`|开发环境专用变量|通常被版本控制|开发模式（如 `npm run dev`）用到|
|`.env.production`|生产环境专用变量|通常被版本控制|生产打包（如 `npm run build`）用到|
|`.env.local`|本地开发专用且不被版本控制的变量|一般添加到 `.gitignore` 忽略|个人本地配置，比如本地调试地址等|

---

### 1. `.env`

基础环境变量文件，定义的变量在所有环境都会生效，除非被其他专门环境的 `.env.*` 文件覆盖。适合放通用配置。

### 2. `.env.development`

只在开发环境下生效。当你执行 `npm run dev` 时，Vue 会自动加载此文件定义的变量。适用于开发时的特定配置，比如本地接口地址。

### 3. `.env.production`

只在生产环境下生效。当你执行 `npm run build` 进行项目构建打包时，Vue 会加载此文件。适合存放正式生产环境下的接口域名、秘钥等配置。

### 4. `.env.local`

本地环境专用，优先级最高，不会被提交到版本库。适合各自开发人员根据自身环境调整一些配置，避免影响他人。

---

## 三、优先级顺序

Vue 按如下优先级加载环境变量：

```plaintext
.env.local > .env.development (开发环境) / .env.production (生产环境) > .env
```

也就是说：

- 开发环境时，优先使用 `.env.local` 中定义的变量，其次是 `.env.development`，最后是 `.env`。
- 生产环境时，优先使用 `.env.local`，其次是 `.env.production`，最后是 `.env`。

例子：

|文件|VITE_API_BASE_URL|
|---|---|
|`.env`|[https://default-url.com](https://default-url.com/)|
|`.env.development`|[http://localhost:3000](http://localhost:3000/)|
|`.env.production`|[https://api.production-url.com](https://api.production-url.com/)|
|`.env.local`|[http://localhost:15421](http://localhost:15421/)|

- 本地开发时，接口地址实际上是 `http://localhost:15421`
- 生产构建时，接口地址是 `https://api.production-url.com`

---

## 四、如何在代码中引用环境变量？

Vue 3 + Vite 中，环境变量名必须以 `VITE_` 开头。例如我们定义：

```ini
VITE_API_BASE_URL=https://api.example.com
```

代码中引用方式：

```js
const baseUrl = import.meta.env.VITE_API_BASE_URL;
console.log('接口地址:', baseUrl);
```

注意：

- `import.meta.env` 是 Vite 提供的访问环境变量的标准方式。
- 不要在 `.env` 文件中写注释或复杂语法，只能简单 `KEY=VALUE` 格式。
- 变量值中，如果包含空格或特殊字符，使用双引号包裹。

---

## 五、常见问题及解决方案

### 1. 本地 `npm run dev` 正常，但打包后请求地址错误

原因通常是你在 `.env.local` 或 `.env.development` 配置了本地接口地址，但在 `.env.production` 中没有正确配置生产接口，导致生产环境请求走了本地地址。

解决办法：

- 确认 `.env.production` 中接口地址正确配置。
- 检查代码中是否动态拼接路径导致路径错误。
- 清理缓存重新打包。

### 2. `.env.local` 配置修改没有生效

确认：

- `.env.local` 文件格式无误，重启开发服务器。
- 变量名以 `VITE_` 开头。
- `.env.local` 在 `.gitignore` 中，避免版本库冲突。

---

## 六、总结

- `.env`：所有环境共享的基础配置
- `.env.development`：开发环境专属配置
- `.env.production`：生产环境专属配置
- `.env.local`：本地环境个性化配置（不提交版本库）

正确利用环境变量配置，可以让项目的开发和部署更灵活、安全，避免因环境差异导致的各种 bug。









