---
title: "在Windows11上安装rust教程"
date: 2025-05-24T19:34:25+08:00
lastmod: 2025-05-24T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- Rust
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

在Windows上安装和使用Rust时，很多新手可能会遇到“找不到Rustup”的问题。实际上，这通常是因为Rustup没有正确安装、没有将其路径加入环境变量，或者环境变量没生效。下面，我们就一步步讲解如何在Windows系统上解决这个问题，并确保你可以顺利运行Rust相关命令。

---

## 一、确认是否已经安装Rustup

打开命令提示符（或者PowerShell），输入：

```shell
rustup --version
```

- 如果显示版本号，比如 `rustup 1.28.2`，说明Rustup已正确安装。
- 如果提示“找不到命令”或错误类似“无法识别为内部或外部命令”，说明需要重新安装或环境变量未设置。

**示例：**

```powershell
PS C:\Users\yourname> rustup --version
rustup 1.28.2
```

如果没有，请继续下一步。

---

## 二、正确安装Rustup

### 方式一：官方推荐安装方法（推荐）

1. 打开浏览器访问 [Rust官方安装页面](https://www.rust-lang.org/tools/install)
2. 下载“rustup-init.exe”
3. 运行程序，然后按照提示安装，默认会把`rustc`、`cargo`等安装到`%USERPROFILE%\.cargo\bin`目录。

**或者可以用PowerShell命令行快速安装：**

```powershell
iwr https://win.rustup.rs -OutFile rustup-init.exe
./rustup-init.exe
```

安装完成后，确认`rustup`版本：

```powershell
rustup --version
```

---

## 三、添加`cargo`路径到系统环境变量

虽然安装时会提示是否添加到PATH，但有时候没有成功。可以手动添加。

### 方法步骤：

1. 右键“此电脑” → 选择“属性”
2. 点击“高级系统设置”
3. 在弹出的“系统属性”窗口中，点击“环境变量”
4. 在“系统变量”区域找到“Path”并点击“编辑”
5. 点击“新建”，添加路径：

```
%USERPROFILE%\.cargo\bin
```

建议直接用完整路径，例如：

```
C:\Users\<你的用户名>\.cargo\bin
```

6. 确认保存，关闭所有窗口。

**注意**：环境变量修改后，建议重新启动终端（PowerShell或命令提示符），使设置生效。

---

## 四、验证环境配置

打开新的PowerShell或命令提示符，输入：

```powershell
rustup --version
rustc --version
cargo --version
```

都能正确显示版本号，比如：

```plaintext
rustc 1.65.0 (abcdef123 2022-03-01)
cargo 1.65.0 (abcdef123 2022-03-01)
```

如果都正常，说明环境已配置成功。

---

## 五、常见问题解决方案

- **`rustup`还是找不到？**
    
    - 先确认环境变量中路径已正确添加，并重新启动终端。
        
    - 可以在命令行中运行：
        
        ```powershell
        echo %Path%
        ```
        
        查看路径是否包含`%USERPROFILE%\.cargo\bin`
        
- **`rustc`报错：`no input filename`**
    
    - 这是因为直接运行`rustc`没有传入源码文件。试试：
        
        ```powershell
        rustc --version
        ```
        
    - 或确认`rustc`已正常安装。
        
- **`rustup`已安装但未在全局生效**
    
    - 再次确认环境变量，并重启终端。

---

## 六、总结

1. 通过官网安装或命令行下载安装`rustup`。
2. 确认`~/.cargo/bin`已加入环境变量。
3. 重启终端，验证是否可以正确使用`rustup`、`rustc`和`cargo`。
4. 如遇问题，检查路径设置和环境变量，确保配置生效。

---

## 附加：安装`Tauri CLI`等工具

一切准备就绪后，就可以用`cargo`或`npm`安装相关工具，例如：

```powershell
npm install -g @tauri-apps/cli
```

或者用`cargo`直接安装：

```powershell
cargo install tauri-cli
```










