---
title: "前端构建工具全解析：NPM、Yarn 和 PNPM"
date: 2025-05-24T18:34:25+08:00
lastmod: 2025-05-24T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- Frontend
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


# 前端构建工具全解析：NPM、Yarn 和 PNPM

## 前言

在现代前端开发中，包管理器（即构建工具）扮演着至关重要的角色。它们帮助开发者管理项目依赖包的安装、版本控制、脚本运行等任务，提高开发效率。本文将详细介绍三大主流的前端包管理器：**NPM**、**Yarn** 和 **PNPM**，帮助你选择合适的工具迎接各种开发场景。

---

## 一、什么是包管理器？

包管理器（Package Manager）是一种工具，用于自动下载安装、更新、删除项目所需的各种软件包（依赖包）。它简化了包的管理流程，确保依赖的版本一致性和项目可维护性。

---

## 二、主流包管理器盘点

### 1. NPM（Node Package Manager）

- **简介**：Node.js 官方自带的包管理器，自Node.js 伴随安装。
- **发布时间**：首次发布于 2010 年。
- **优势**：
    - 官方支持，与 Node.js 深度集成。
    - 生态最为庞大，拥有最大的包库（npm Registry）。
    - 易用性强，熟悉度高。
- **不足**：
    - 依赖安装速度相对较慢（早期版本）。
    - 有时会出现“包锁”相关的版本冲突问题（已改善）。

### 2. Yarn

- **简介**：由 Facebook 于 2016 年推出，旨在解决 NPM 在性能和安全上的不足。
- **发布时间**：2016 年。
- **优势**：
    - **更快的依赖安装速度**（通过缓存和并行安装）。
    - **更强的依赖一致性**（锁文件 `yarn.lock` 更稳定）。
    - 支持 **离线模式**。
    - 具有 **工作空间（Workspaces）** 支持，方便 monorepo（多包仓库）管理。
- **不足**：
    - 需要额外安装（虽然也支持通过 `corepack` 直接用）。

### 3. PNPM

- **简介**：由 Zoltan Kochan 创建，诞生于 2016 年，用不同的方式管理依赖，更加高效。
- **优势**：
    - **硬链接技术**：多个项目共用相同依赖的硬链接，节省磁盘空间。
    - **性能优异**：安装速度快，尤其是在 monorepo 环境中。
    - **严格的依赖隔离**，避免“依赖污染”。
    - 兼容 NPM 和 Yarn 的命令。
- **不足**：
    - 学习曲线稍陡（需要理解硬链接和模块隔离机制）。
    - 生态圈还在发展中，但支持程度已逐渐成熟。

---

## 三、详细对比

|特性|NPM|Yarn|PNPM|
|---|---|---|---|
|发布年份|2010|2016|2016|
|安装速度|正常|更快|极快|
|依赖稳定性|较好|更优|极佳（严格隔离）|
|依赖缓存|支持|支持|支持|
|多包仓库（monorepo）|支持（v7+）|原生支持|原生支持|
|依赖隔离机制|符合NPM规范|符合NPM规范|使用硬链接，不污染依赖|
|磁盘空间利用|普通|依赖缓存，节省空间|极大节省（硬链接）|
|跨平台支持|全平台|全平台|全平台|
|社区支持|最大，最成熟|广泛，活跃|快速增长，越来越��|

---

## 四、实际使用建议

- **新项目建议**：如果你是新手或希望使用最官方、最普遍的工具，建议选择 **NPM**（最新版已大幅提升性能和稳定性）。
- **性能优先**：如果强调速度和资源节约，**PNPM** 是最佳选择，特别适合大型 monorepo 和重复依赖的项目。
- **团队协作**：如果团队已使用 Yarn，有复杂的依赖管理需求或需要离线安装支持，也可选择 Yarn。

---

## 五、安装示例

### 安装 NPM（已自带 Node.js）

```bash
# 无需额外安装，安装 Node.js 就包含了 NPM
node -v
npm -v
```

### 安装 Yarn

```bash
npm install -g yarn
# 或使用 corepack
corepack enable
```

### 安装 PNPM

```bash
npm install -g pnpm
```

---

## 六、常用基本命令对比

|操作|NPM|Yarn|PNPM|
|---|---|---|---|
|初始化项目|`npm init`|`yarn init`|`pnpm init`|
|安装依赖|`npm install pkg`|`yarn add pkg`|`pnpm add pkg`|
|安装开发依赖|`npm install -D pkg`|`yarn add -D pkg`|`pnpm add -D pkg`|
|移除依赖|`npm uninstall pkg`|`yarn remove pkg`|`pnpm remove pkg`|
|更新依赖|`npm update`|`yarn upgrade`|`pnpm update`|
|安装所有依赖（恢复）|`npm install`|`yarn install`|`pnpm install`|

---

## 七、总结

|工具|特色|适用场景|
|---|---|---|
|**NPM**|官方最早、最普遍、生态最大|入门、广泛使用，无特殊需求即可用|
|**Yarn**|更快、更稳定、支持工作空间|有复杂依赖管理需求的中大型项目|
|**PNPM**|高性能、节省空间、严苛隔离|大型 monorepo、追求极致效率的团队|


# 深入了解Monorepo：概念、技术与生态全解析

在现代前端和多模块项目开发中，“Monorepo”逐渐成为一种流行的管理方案。它通过将多个子项目集中在一个仓库中，实现依赖共享、模块复用和统一管理，但同时也带来了新的管理挑战。本文将详细介绍什么是Monorepo，它与主流包管理工具（如 npm、Yarn 和 pnpm）的关系，以及当前生态中的技术方案和工具链。

---

## 一、什么是Monorepo？

**定义**：  
“Monorepo”全称为“Mono Repository”，即“单一仓库”的意思，指在一个版本控制仓库（如 Git）中存放多个相关子项目或包，例如多个前端应用、库或服务的集合。

**核心思想**：

- 将多个相关项目集成在一个仓库中
- 共享依赖和代码
- 统一版本控制与发布流程
- 简化依赖管理与跨项目协作

**优点**：

- 依赖版本统一，避免版本冲突
- 增强代码复用和整合测试
- 简化跨模块开发与维护
- 支持集中式CI/CD流程

**缺点**：

- 仓库变大，管理复杂度增加
- 构建时间可能变长（需优化）
- 需要特殊工具支持依赖和构建管理

---

## 二、包管理工具与Monorepo的关系

现代包管理器（NPM、Yarn、pnpm）都在不断强化对“工作区（workspace）”的支持，使其可以更好地服务于Monorepo结构。

|工具|支持工作区（Workspace）|促进Monorepo的作用|
|---|---|---|
|**NPM**|从v7开始正式支持|通过`workspaces`字段管理多个子包，逐渐改善Monorepo支持|
|**Yarn**|原生支持（Workspaces）|早期主导Monorepo方案，支持灵活的依赖共用、管理|
|**PNPM**|原生支持（Workspaces）|利用硬链接，极大节省空间，实现高效的依赖复用|

包管理器在Monorepo中的主要作用：

- 管理多个子项目的依赖安装
- 实现依赖的共享和隔离
- 简化版本控制和依赖同步
- 支持跨项目的快速构建和测试

实际上，**Monorepo**并不是一套具体技术，而是一种“管理理念”，具体的实践需要借助合适的工具链实现。

---

## 三、Monorepo生态现状与技术方案

### 1. 生态现状

- **缺乏统一标准**：目前大多依赖辅助工具，尚无“一统天下”的框架。
- **工具多样**：常用的方案包括pnpm+workspaces、Yarn workspaces、Lerna、Turborepo，结合使用以优化开发体验。
- **生态特点**：
    - 许多方案集中在“库”的管理，缺少完善的“完整框架”支持。
    - 工具更多像“辅助工具”或“脚手架”，非全自动的完整解决方案。
    - 未来趋势可能会向“完整框架”演进，例如NX、Turborepo，或包管理器原生支持更多功能。

### 2. 核心技术与方案

|方案|特点|作用与优势|
|---|---|---|
|**npm + workspaces**|最新版本支持（v7+），但成熟度和效率有限|基础方案，兼容性好，但速度和空间优化不足|
|**Yarn (Berry)**|早期支持workspaces，持续优化，支持PnP（零依赖）|高速、丰富特性，适应复杂的多包管理场景|
|**pnpm**|基于硬链接和全局缓存，空间和速度双优|极致性能，节省空间，硬隔离，适合大型monorepo管理|

## 四、主流Monorepo管理方案详解

### 1. **pnpm + workspaces**

**优势**：

- 速度快：硬链接技术让依赖安装几乎瞬时完成。
- 节省空间：依赖只存储一份，通过硬链接在多个项目间共享。
- 简单配置：只需在根目录创建`pnpm-workspace.yaml`文件，定义包路径。
- 高度兼容：支持多语言、多框架环境。

**示例配置**：

```yaml
# pnpm-workspace.yaml
packages:
  - 'packages/*'
  - 'libs/*'
```

### 2. **Yarn Workspaces**

**特点**：

- 原生支持：在`package.json`中定义`workspaces`字段。
- 丰富功能：支持 `nohoist`等配置，避免部分依赖被提升到根目录。
- 常与Lerna结合：实现版本管理与发布自动化。

**示例配置**：

```json
{
  "private": true,
  "workspaces": ["packages/*", "libs/*"]
}
```

### 3. **Lerna**

早期最流行的Monorepo管理工具，专注于：

- 多包版本控制
- 依赖管理
- 发布自动化

**特点**：

- 与 npm, Yarn, pnpm 兼容
- 适合大规模仓库的版本发布

### 4. **Turborepo**

由Vercel推出，专注于：

- **增量构建**：只构建变更部分
- **缓存机制**：复用中间结果
- **多语言、多框架支持**  
    适合快速、高效的大型项目管理。

---

## 五、总结：打造高效的Monorepo实践

- **工具选择**：
    
    - 小型项目或追求简单：`pnpm` + `workspaces`
    - 复杂依赖关系和版本控制：`Yarn` + `Lerna`
    - 全面构建加速：`Turborepo`
- **最佳实践建议**：
    
    - 明确项目边界，划分合理的子模块
    - 使用统一的依赖管理策略
    - 配置增量构建与缓存机制
    - 自动化CI/CD流程，保证版本一致性

---

## 六、未来趋势展望

未来，**Monorepo**可能逐渐演变为：

- 更完备的“完整生态链”，集依赖管理、构建、测试、发布于一体
- **包管理器原生支持**：像pnpm或npm未来可能会原生加入更多Monorepo管理能力
- **集中式开发平台**：整合IDE、构建、依赖管理，提升团队协作效率

---

## 七、总结

- **Monorepo**作为一种仓库管理思想，旨在集中管理多个相关项目，提升开发效率与依赖一致性。
- **核心技术**：依赖管理（pnpm、Yarn、npm）、任务管理（Turborepo、Lerna）和结构组织（工作区、子目录）。
- **实践路径**：
    - 选择合适工具（如pnpm+workspaces）
    - 结构合理划分模块
    - 自动化流程优化整体开发体验

充分利用Monorepo的优势，结合强大的工具链，可以极大提高前端和多模块项目的开发效率和可维护性。

原文链接：[示例链接](https://blog.csdn.net/m0_63472757/article/details/147297282)


# PNPM及其常用命令

## 一、什么是pnpm？

`pnpm`（Performant NPM）是一款高性能的 Node.js 包管理工具，它通过创新的硬链接技术和全局内容存储，大幅提升依赖安装速度并减少磁盘空间占用。

**核心优势：**

- **安装速度快**：依赖基础包只存储一份，通过硬链接链接到每个项目。
- **节省空间**：重复依赖只存储一次，多个项目共享依赖内容。
- **依赖隔离**：确保每个项目的依赖版本一致，避免依赖污染。
- **兼容性好**：支持`package.json`的全部语法和大部分npm生态工具。

---

## 二、pnpm常用命令详解

### 1. `pnpm install`

- **作用**：根据项目中的`package.json`和`pnpm-lock.yaml`（如果存在）安装所有依赖。
- **常用场景**：
    - 克隆新项目后，安装所有依赖
    - 依赖升级后，重新同步
    - 在没有添加新依赖时，保持依赖一致
- **示例**：
    
    ```bash
    pnpm install
    ```
    
- **特点**：不会修改`package.json`或`pnpm-lock.yaml`，只负责“安装”。

---

### 2. `pnpm add <package> [<package> ...]`

作用：

- 安装一个或多个包，并自动把它们添加到`dependencies`（默认）或`devDependencies`（使用`-D`或`--save-dev`）中。

常用场景：

- 添加新依赖
- 添加开发依赖（如测试、构建工具）

示例：

```bash
# 添加生产依赖（默认）
pnpm add react axios lodash

# 添加开发依赖（如测试工具）
pnpm add -D jest tsx
```

其他用法比如指定版本：

```bash
pnpm add vue@3.2.0
```

---

### 3. `pnpm remove <package>`

- **作用**：从`dependencies`或`devDependencies`中删除指定包，并同步`package.json`。
- **示例**

```bash
pnpm remove lodash
```

---

### 4. `pnpm update [<package>]`

- **作用**：更新项目中安装的依赖（全部或指定包）。
- **示例**

```bash
pnpm update             # 更新所有包
pnpm update react     # 只更新react包
```

---

### 5. 其他常用命令

|命令|作用|备注|
|---|---|---|
|`pnpm list`|查看项目所有已安装的依赖|可以用 `pnpm ls` 简写|
|`pnpm dedupe`|尝试去除依赖冗余，输出更扁平的依赖树|有助优化依赖结构|
|`pnpm prune`|移除未使用的依赖|类似`npm prune`|
|`pnpm run <script>`|运行`scripts`中的脚本|与`npm run`类似|

---

## 三、`pnpm`与`npm`的区别

|特点|`pnpm`|`npm`|
|---|---|---|
|存储机制|使用硬链接，依赖全局存储，节省空间|每个项目存一份 `node_modules`|
|安装速度|更快|相对较慢|
|磁盘空间|占用更少|占用较多|
|依赖隔离|更严格，避免“依赖污染”|容易嵌套依赖冲突|
|兼容性|极佳，支持`package.json`规范|广泛，成熟|

**总结**：pnpm 在性能、空间和依赖隔离方面优于传统的`npm`，特别适合多项目或大规模开发环境。

---


# PNPM配置存储路径

关于配置pnpm的存储路径（`store-dir`）以及相关参数，很多用户会遇到配置成功或未生效的问题。为帮助你清晰理解和正确设置，整理如下内容：

---

## 1. `pnpm`存储位置的基本原理

- `pnpm`默认将所有缓存和包存储在系统特定的路径里，比如`%LOCALAPPDATA%\pnpm\store\vX`。
- 你可以通过`pnpm config`命令自定义`store-dir`，把存储路径指向你希望的位置。

## 2. 常见问题：为什么`pnpm config get store-dir`返回`undefined`？

- 这是因为`store-dir`配置未在**全局配置层级**设置成功，或者配置没有正确保存。
- 另外，`pnpm store path`显示的路径是**实际存储路径**，可能与你设置的`store-dir`不同，尤其是没有正确配置时，会显示默认路径。

## 3. 正确配置存储路径的方法

### 方法一：用`pnpm config set`命令（推荐）

```bash
pnpm config set store-dir D:\pnpm-store --global
```

- 这会将存储路径设置为`D:\pnpm-store`（可以改成你喜欢的路径）。
- 参数`--global`确保是设置到全局配置。

如果不生效就执行下面的命令：

```bash 
pnpm config --location=global set store-dir D:\pnpm-package\.pnmp-store 
```

### 方法二：确认配置已成功

```bash
pnpm config get store-dir
```

- 如果输出你的路径，配置成功；如果是`undefined`，说明没有生效。

### 方法三：查看全部配置确认层级

```bash
pnpm config list --json
```

- 查看所有配置项，确认`store-dir`在其中。

### 方法四：直接编辑配置文件（可选）

- 全局配置文件通常在：
    
    ```
    %APPDATA%\pnpm\config.yaml
    ```
    
- 打开这个文件，添加或修改：
    
    ```yaml
    store-dir: D:\pnpm-store
    ```
    
- 保存后重新加载终端。
    

## 4. 验证配置是否生效

- 运行：

```bash
pnpm store path
```

- 这会显示pnpm实际使用的存储路径。如果你之前正确设置`store-dir`，结果应该是你自定义的路径。

## 5. 其他相关参数（可选）

- `cache-dir`：缓存目录，可以用来加快依赖安装，也可以配置。
- `global-dir`：全局包的存放目录。
- `registry`：仓库源地址。
- `state-dir`：存储pnpm的状态信息（一般默认即可）

**示例配置：**

```bash
pnpm config set cache-dir D:\pnpm-cache --global
pnpm config set global-dir D:\pnpm-global --global
pnpm config set registry https://registry.npmmirror.com --global
```

如果不生效就修改`--global`为`--location=global`。
## 6. 结语

- 你可以根据需要自定义存储路径，提升缓存管理效率。
- 配置成功后，确保用`pnpm store path`验证实际路径是否符合预期。
- 若出现设置无效，建议用`pnpm config list --json`确认配置是否正确，或直接编辑配置文件。










