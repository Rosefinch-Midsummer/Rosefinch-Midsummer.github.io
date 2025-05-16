---
title: "Redis安装教程（含Linux和Windows系统）"
date: 2025-05-16T12:34:25+08:00
lastmod: 2025-05-16T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- 数据库
- Redis
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

# Linux 系统安装 Redis

本文介绍如何在 Linux 系统上安装 Redis，适用于 Redis Community Edition 和 Redis Stack 7.x 版本。  
目前大多数主流 Linux 发行版都提供了 Redis 的安装包。

---

## 在 Ubuntu/Debian 上安装 Redis

1. 添加 Redis 官方软件源，并更新 APT 源：

```bash
sudo apt-get install lsb-release curl gpg
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
sudo chmod 644 /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
sudo apt-get update
```

2. 安装 Redis：

```bash
sudo apt-get install redis
```

安装完成后，Redis 服务会自动启动，并设置为开机自启。

如果系统重启后 Redis 未自动启动，可以手动启用：

```bash
sudo systemctl enable redis-server
sudo systemctl start redis-server
```

---

## 后台启动和停止 Redis

在 Ubuntu/Debian（使用 apt 安装）以及 Red Hat/Rocky（使用 yum 安装）系统中，可以使用 `systemctl` 命令控制 Redis 服务的启动和停止。

- 启动 Redis 服务：

```bash
sudo systemctl start <redis-service-name>
```

其中 `<redis-service-name>` 可能是 `redis` 或 `redis-server`，具体名称取决于发行版。

- 停止 Redis 服务：

```bash
sudo systemctl stop <redis-service-name>
```

---

## 连接和测试 Redis

Redis 服务启动后，可以使用命令行工具 `redis-cli` 连接测试：

```bash
redis-cli
```

连接成功后，输入命令 `ping`，如果返回 `PONG`，说明 Redis 运行正常：

```
127.0.0.1:6379> ping
PONG
```

此外，你还可以使用 [Redis Insight](https://redis.io/docs/latest/develop/tools/insight/) 图形化工具，方便地管理和监控 Redis 服务器。

# Windows 系统安装 Redis 7.4 教程

> 原文链接：[window 安装redis7.4](https://www.cnblogs.com/lanjianhua/p/18383752) （发布于 2024-08-27）

---

## 前言

Windows 平台上 Redis 有多个版本，了解不同版本的区别可以参考：[Msys/MinGW 与 Cygwin/gcc 简介](https://blog.zengrong.net/post/msys_mingw_and_cygwin_gcc/)。  
本文使用的是 `Redis-7.4.0-Windows-x64-msys2-with-Service.zip`（msys2 版本）。

示意图：  
![Redis](https://img2024.cnblogs.com/blog/3498501/202408/3498501-20240827234650923-683688286.png)

---

## 下载地址

- GitHub 官方发布页：  
    [https://github.com/redis-windows/redis-windows/releases](https://github.com/redis-windows/redis-windows/releases)
    
- Redis 7.4.0 版本下载链接：  
    [https://github.com/redis-windows/redis-windows/releases/download/7.4.0/Redis-7.4.0-Windows-x64-msys2-with-Service.zip](https://github.com/redis-windows/redis-windows/releases/download/7.4.0/Redis-7.4.0-Windows-x64-msys2-with-Service.zip)
    

---

## 安装步骤

1. **解压**下载的压缩包 `Redis-7.4.0-Windows-x64-msys2-with-Service.zip`。
    
2. **重命名文件夹**  
    将解压后的文件夹 `/Redis-7.4.0-Windows-x64-msys2-with-Service` 重命名为 `Redis-7.4.0`，作为 Redis 的根目录。
    
3. **进入根目录**  
    打开 `Redis-7.4.0` 文件夹。
    
4. **安装 Redis 服务**  
    找到 `install_redis_service.bat` 文件，点击鼠标右键，选择“以管理员身份运行”。
    
    _(此操作会将 Redis 设置为系统服务)_
    
5. **输入安装路径**  
    安装程序弹出控制台，提示输入 Redis 安装路径时，将刚才解压的根目录路径粘贴进去（例如：`E:\Redis-7.4.0`），然后回车确认。
    
6. **输入配置文件路径**  
    继续输入 Redis 配置文件（`redis.conf`）所在路径，直接输入并回车确认，路径同上。
    
7. **完成安装**  
    程序提示“按任意键完成”，按下任意键结束安装。
    
8. **配置环境变量**  
    将 Redis 安装目录添加到系统环境变量 `Path` 中，方便命令行直接调用 Redis 命令。
    
    配置示例图：  
    ![环境变量配置](https://img2024.cnblogs.com/blog/3498501/202408/3498501-20240828000736261-2087323872.png)
    
9. **检查服务状态**
    
    - 使用快捷键 `Win + R`，输入 `services.msc`，回车，打开“服务”管理窗口。
    - 查找名为 “Redis” 的服务，确认服务是否存在且已启动。
    
    服务界面示例：  
    ![Redis 服务](https://img2024.cnblogs.com/blog/3498501/202408/3498501-20240827234257599-2099340754.png)
    
10. **测试服务是否运行正常**
    
    - 按 `Win + R`，输入 `cmd`，打开命令行窗口；
    - 输入 `redis-cli`，按回车；
    - 输入命令 `ping`，按回车。
    - 如果返回 `PONG`，代表 Redis 服务正常。
    
    测试示例：  
    ![Redis ping](https://img2024.cnblogs.com/blog/3498501/202408/3498501-20240827234221750-1838548811.png)
    

---

## 常用 Redis 服务命令（管理员权限 cmd 窗口）

- 启动 Redis 服务：
    
    ```
    net start redis
    ```
    
- 停止 Redis 服务：
    
    ```
    net stop redis
    ```
    
- 删除 Redis 服务：
    
    ```
    sc delete redis
    ```
    

---

## 完成！

至此，Windows 下 Redis 7.4 安装及服务配置完成！


# Tiny RDM：你的下一代 Redis 桌面 GUI 神器

作者：Lykin（Tiny RDM 开源项目作者）  

[来源网址](https://zhuanlan.zhihu.com/p/679727630)

---

## 简介

对于频繁使用 Redis 的用户来说，选择一个顺手的图形化界面工具，可以大幅提升操作效率，避免繁琐的命令行操作。  

**Tiny RDM（Tiny Redis Desktop Manager）** 正是一款桌面端的 Redis 客户端，它具有“开源、免费、高颜值、跨平台、轻量且功能齐全”的优势，丝毫不输市场上主流的同类产品。

官方主页：[redis.tinycraft.cc/zh/](https://redis.tinycraft.cc/zh/)  

源码地址：[github.com/tiny-craft/tiny-rdm](https://github.com/tiny-craft/tiny-rdm)


---

## 主界面展示

![](https://pic3.zhimg.com/v2-17203bbf3a7dbd2b20a1c06443151c56_1440w.jpg)

---

## 功能特色

- **极致轻量且跨平台**  
    支持 macOS、Windows 和 Linux 三大操作系统。所有平台安装包均约 10MB，轻松安装，随时随地使用。
    
- **现代化界面设计**  
    界面简洁美观，符合现代审美，支持浅色和深色主题自由切换。
    
- **多样的登录方式与个性化连接配置**  
    支持 SSH、SSL、哨兵模式和集群登录，提供丰富的个性化连接选项满足不同需求。
    
- **多种格式灵活查看**  
    内置高级文本代码编辑器，支持语法高亮、代码折叠、错误提示等功能，轻松编辑并保存加密或压缩格式内容。
    
- **便捷的搜索与过滤**  
    支持使用正则表达式进行键值搜索，且可进行二级筛选，组合过滤数据更加高效。
    
- **支持海量键值加载**  
    通过分段加载机制，轻松应对千万级键值量，支持外部键列表以及复杂数据类型（如 List、Hash、Set、ZSet、Stream）的内部值加载。
    
- **批量数据操作**  
    键列表支持多选，提供导入导出、多选删除、基于正则表达式的批量删除、批量 TTL 更新等实用功能。
    
- **丰富的调试与分析支持**  
    包含命令行执行、慢日志查询、服务器命令实时监控、发布/订阅功能，大大提升开发和调试效率。
    
- **贴心细节功能**  
    支持数据库别名、自动刷新、TTL 可读性展示、二进制键显示、多彩数据类型图标、便捷的 TTL 设置标签等。开发团队相信，细节虽难被肉眼捕捉，但用心的人定能感受到。
    

---

## 安装及下载

> Github 下载地址：  
> [github.com/tiny-craft/tiny-rdm/releases](https://github.com/tiny-craft/tiny-rdm/releases)  
> 官方微信公众号「独立开发记事簿」，输入关键字：**下载RDM**

> **特别提示：**  
> 目前官方未与任何渠道合作发布版本，请务必通过官方仓库或微信公众号下载，或自行编译源码安装。避免使用来路不明的安装包，以免造成不必要的损失，官方不承担相关责任。

---

## 结语

Tiny RDM 功能强大且易用，完全满足日常开发与运维对 Redis 客户端的需求。这是一个由热爱开发的开源作者团队无偿维护的项目，欢迎大家在 Github issue 反馈建议和问题。希望能为国产开源项目贡献力量，并为广大开发者带来价值。









