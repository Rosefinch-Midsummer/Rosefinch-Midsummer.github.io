---
title: "OpenSSL 详解及安装教程"
date: 2025-06-02T12:34:25+08:00
lastmod: 2025-06-03T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- OpenSSL
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

# OpenSSL详解及安装教程

## 一、什么是OpenSSL？

OpenSSL是一个开源且功能丰富的安全工具库，主要用于实现SSL/TLS协议，保障网络通信的机密性和完整性。它诞生于Netscape提出的SSL（Secure Sockets Layer）协议基础之上，现已成为互联网安全通信的工业标准。

### OpenSSL的核心功能包括：

- **SSL协议实现**：支持SSLv2、SSLv3和TLSv1等多种协议版本。
- **加密算法库**：涵盖对称加密、非对称加密、摘要算法。
- **大数运算**：支持复杂的数学运算，用于密码学计算。
- **密钥生成**：支持非对称算法的密钥对生成。
- **证书处理**：包括ASN.1编解码、PKCS#10证书请求、数字证书和CRL（证书吊销列表）编解码。
- **在线证书状态协议（OCSP）**：证书状态验证。
- **支持多种数字证书标准**：如PKCS7、PKCS12格式证书的读取和生成。

### 开发语言与跨平台支持

OpenSSL使用**C语言**开发，保证了出色的性能和广泛的跨平台兼容性。目前支持的主要平台包括：

- Linux
- UNIX
- Windows
- macOS

你可以在其[GitHub仓库](https://github.com/openssl/openssl)查看项目源码和文档。

---

## 二、OpenSSL工具箱主要组件

OpenSSL整体由三个核心部分组成：

1. **openssl**：提供了多功能的命令行工具，用于加密、解密、密钥生成、证书管理等。
2. **libcrypto**：实现各种加密算法的加密库。
3. **libssl**：实现SSL及TLS协议的加密模块库。

---

## 三、下载与安装OpenSSL

对于不想自行编译源码的用户，推荐下载预编译的Windows安装包，操作简单快捷。

### 1. 获取安装包

访问Win32/Win64 OpenSSL官方镜像站点：

[http://slproweb.com/products/Win32OpenSSL.html](http://slproweb.com/products/Win32OpenSSL.html)

主要有以下四种安装包：

|安装包名称|说明|
|---|---|
|Win64 OpenSSL v1.1.1i Light|精简版，Win64常用|
|Win64 OpenSSL v1.1.1i|完整版，Win64使用|
|Win32 OpenSSL v1.1.1i Light|精简版，Win32常用|
|Win32 OpenSSL v1.1.1i|完整版，Win32使用|

**建议选择**：`Win64 OpenSSL v1.1.1i`完整版（根据你的系统架构选择32/64位版本）。

### 2. 安装步骤

1. 双击下载好的安装程序（例如 `Win64OpenSSL-1_1_1i.exe`）启动安装向导。
2. 大多数默认选项可直接采用。
3. 安装过程中会提示选择**OpenSSL的DLL文件拷贝位置**，建议选择**安装目录下**（不要复制到系统目录）。原因是避免与系统或其他软件自带的OpenSSL版本冲突。
4. 安装完成后，会询问是否捐款，用户可根据个人意愿选择。

### 3. 安装目录结构

安装完成后，目录中主要包含：

- `bin`目录：包含`openssl.exe`工具和相关DLL文件。
- `lib`目录：静态和动态库文件。
- `include`目录：头文件。
- 其他配置文件和文档。

---

## 四、环境配置与使用验证

### 1. 配置环境变量（可选）

为了在命令行直接调用`openssl`工具，需要将OpenSSL的`bin`目录加入系统环境变量`Path`中。

- Windows系统：  
    右击【此电脑】→【属性】→【高级系统设置】→【环境变量】→编辑`Path`，添加`OpenSSL


### 2. 验证安装是否成功

安装完成并配置环境变量后，打开命令提示符（CMD）或PowerShell，输入以下命令检查OpenSSL版本：

```bash
openssl version
```

如果正确安装，会显示类似如下版本信息：

```
OpenSSL 1.1.1i  8 Dec 2020
```

这说明OpenSSL安装成功，可以正常使用。

---

## 五、Visual Studio 中调用 OpenSSL 的配置示例

如果你在Windows平台使用Visual Studio进行开发，并调用OpenSSL库，以下为配置步骤示例（以VS2017为例）：

1. **包含目录设置**  
    在项目属性页中，选择【VC++目录】→【包含目录】，添加OpenSSL的`include`文件夹路径。例如：
    
    ```
    C:\OpenSSL-Win64\include
    ```
    
2. **库目录设置**  
    在【VC++目录】→【库目录】添加OpenSSL的`lib`目录路径，例如：
    
    ```
    C:\OpenSSL-Win64\lib
    ```
    
3. **链接器设置**  
    在【链接器】→【输入】→【附加依赖项】，添加以下库文件：
    
    ```
    libcrypto.lib
    libssl.lib
    ```
    
4. **复制DLL文件**  
    确保编译后的可执行文件所在目录能找到OpenSSL的DLL文件（一般在`bin`目录），可将`bin`目录中的dll复制到项目的输出目录，或将`bin`加入系统环境变量`Path`。
    

完成以上配置后，即可在代码中调用OpenSSL的相关API。

---

## 六、常见问题及解决方案

### 1. 编译Rust项目时出错：`error: failed to run custom build command for openssl-sys`

这是Rust项目中依赖OpenSSL时，编译无法找到合适的OpenSSL库引起的错误。解决方法有：

- 确保系统中已正确安装OpenSSL，并配置了相应的环境变量（包含`bin`, `include`, `lib`路径）
    
- 对于Windows用户，建议安装“Win64 OpenSSL”安装包，并把`bin`目录加到环境变量`Path`中
    
- 在项目中可通过设置环境变量告知编译器OpenSSL路径，例如：
    
    ```bash
    set OPENSSL_DIR=C:\OpenSSL-Win64
    set OPENSSL_LIB_DIR=C:\OpenSSL-Win64\lib
    set OPENSSL_INCLUDE_DIR=C:\OpenSSL-Win64\include
    ```
    
- 使用包管理工具或Rust工具链专门配置OpenSSL依赖，避免版本不匹配问题。
    

---

## 七、总结

OpenSSL作为开源的加密算法库和SSL/TLS实现工具，广泛用于网络安全和应用加密中。它拥有丰富的功能和良好的跨平台性能，是开发安全通信应用的基石。

本文介绍了OpenSSL的基本功能，Windows下的下载安装和配置流程，以及常见环境配置和问题解决方法。掌握这些知识，有助于开发者快速将OpenSSL集成进项目，提高系统安全性。

## 参考资料

[OpenSSL-Windows版下载地址](https://slproweb.com/products/Win32OpenSSL.html)

[Windows系统安装OpenSSL(安装包方式）](https://blog.csdn.net/u010333084/article/details/136562246)

[解决在 Windows 上 openssl-sys 构建失败的问题](https://www.z2blog.com/archives/jie-jue-zai-windows-shang-openssl-sys-gou-jian-shi-bai-de-wen-ti)







