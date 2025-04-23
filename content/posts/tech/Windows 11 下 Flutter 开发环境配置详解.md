---
title: "Windows 11 下 Flutter 开发环境配置详解"
date: 2025-04-23T18:34:25+08:00
lastmod: 2025-04-23T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- Flutter
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


# Windows 11 下 Flutter 开发环境配置详解

## 前言

Flutter 是 Google 推出的开源 UI 框架，用于开发跨平台应用程序。它允许开发者使用一套代码库，构建适配 Android、iOS、Web 以及 Windows、macOS 与 Linux 等桌面平台的高性能原生应用。凭借其丰富的组件库和高效的渲染引擎，Flutter 正日益成为移动端及桌面端应用开发的热门选择。

本文将针对 Windows 11 系统，详细介绍 Flutter 开发环境的搭建流程，涵盖常见报错的解决方案，帮助开发者顺利完成环境配置并成功运行第一个 Flutter 项目。

参考资料：[Flutter 在 Windows 下的开发环境搭建（Flutter SDK 3.19.2）【图文详细教程】](https://segmentfault.com/a/1190000044767999)

核心理念：`flutter doctor`报错信息提示需要什么就下载什么。

配置好Flutter环境，再执行`flutter doctor`会出现如下界面：

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost05/img20250423143518.png)


## 正文

### 一、下载安装 Flutter SDK

1. 访问官方文档 [Flutter Windows 安装指南](https://docs.flutter.dev/get-started/install/windows)。
2. 下载最新的 Flutter SDK 压缩包。
3. 解压到你习惯的目录（建议带上版本号做区分，例如 `D:\flutter_sdk\flutter_3.19.2`）。
4. 将 Flutter SDK `bin` 目录添加到系统环境变量 `Path` 中：
   - 右键“此电脑”→“属性”→“高级系统设置”→“环境变量”
   - 找到系统变量中的 `Path`，点击“编辑”→“新建”，添加 Flutter SDK `bin` 路径，例如：`D:\flutter_sdk\flutter_3.19.2\bin`

### 二、解决 Flutter Doctor 网络连接超时问题

执行命令：

```bash
flutter doctor
```

可能出现如下错误：

```
[!] Network resources
    ✗ A network error occurred while checking "https://maven.google.com/": Operation timed out
    ✗ An HTTP error occurred while checking "https://github.com/": Operation timed out
```

#### 1. 设置 Git 代理解决 GitHub 访问

如果你使用代理（比如 Shadowsocks、V2Ray 等），使用以下命令设置 Git 代理：

```bash
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

> 注意修改端口号为你本地代理端口。

#### 2. 替换 Flutter 使用的 Maven 镜像为阿里云源

Flutter 默认访问 `https://maven.google.com/`，容易超时。替换为国内阿里云镜像：

- 进入 Flutter SDK 根目录
    
- 打开 `packages/flutter_tools/lib/src/http_host_validator.dart`
    
- 找到如下代码：
    
    ```dart
    const String kMaven = 'https://maven.google.com/';
    ```
    
- 修改为：
    
    ```dart
    const String kMaven = 'http://maven.aliyun.com/nexus/content/groups/public/';
    ```
    
- 删除 Flutter 缓存：

```bash
rd /s /q bin\cache
```

注意这里删除的是`flutter/bin`下面的`cache`文件夹

- 重新打开命令行执行 `flutter doctor`，网络错误应消失。

### 三、安装 Android Studio 及配置 Android SDK

Flutter 开发 Android 应用必须安装并配置好 Android Studio。

1. 下载地址：[Android Studio 官网](https://developer.android.com/studio)
2. 安装后，首次启动会提示下载 Android SDK 及相应组件。
3. 进入 Android Studio 设置页面：
    - `File` → `Settings` → `Appearance & Behavior` → `System Settings` → `Android SDK`
    - 在 SDK Platforms 里选择合适的 Android 版本
    - 点击 SDK Tools 选项卡，勾选并安装 **Android SDK Command-line Tools（latest）**
4. 若 Flutter 提示找不到 Android SDK，手动指定 SDK 路径：

```bash
flutter config --android-sdk <你的Android SDK路径>
```

5. 接受 Android 许可协议：

```bash
flutter doctor --android-licenses
```

在提示时多次输入 `y` 以同意。

### 四、安装 Google Chrome

Flutter Web 开发需要 Chrome 浏览器。

- 下载地址：[Google Chrome 官网](https://www.google.cn/chrome/index.html)
- 安装后，如果 `flutter doctor` 提示找不到 Chrome，可手动指定环境变量 `CHROME_EXECUTABLE` 指向 Chrome 路径。

### 五、安装 Visual Studio

开发 Windows 桌面应用需要安装 Visual Studio，并选择 **“使用 C++ 的桌面开发”** 工作负载。

1. 下载地址：[Visual Studio 官网](https://visualstudio.microsoft.com/downloads/)
2. 建议安装“社区版”即可
3. 安装时务必勾选“Desktop development with C++”
4. 安装完成重启电脑。

### 六、配置 Flutter 访问国内镜像避免下载问题

部分用户会遇到对 `https://storage.googleapis.com/` 的访问失败，错误如下：

```
A cryptographic error occurred while checking "https://storage.googleapis.com/": Connection terminated during handshake
```

解决方法：

- 新建系统环境变量：
    
    ```
    变量名：FLUTTER_STORAGE_BASE_URL
    变量值：https://storage.flutter-io.cn
    ```
    
- 关闭并重新打开命令行，再执行 `flutter doctor`
    

### 七、创建并运行第一个 Flutter 项目

1. 选择一个项目文件夹，在命令行输入：

```bash
flutter create first_flutter_project
```

> 项目名只允许使用下划线，不允许破折号。

2. 进入项目目录：

```bash
cd first_flutter_project
```

3. 运行项目：

```bash
flutter run
```

如果连接了安卓设备或者模拟器，将可以看到 Flutter Demo 应用成功启动。

使用`flutter run -v`会显示具体运行信息。

---

## 总结

Windows 11 下 Flutter 环境的配置主要包括：下载 Flutter SDK、配置环境变量、解决网络代理及国内镜像源问题、安装并配置 Android Studio、Chrome 和 Visual Studio。遇到报错时分别针对网络、许可协议等问题逐步排查解决，即可顺利完成开发环境搭建。最后，执行 `flutter create` 并运行示例项目进行验证，确认环境搭建成功。

祝你玩转 Flutter，打造跨平台的精彩应用！







