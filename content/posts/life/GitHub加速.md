---
title: "GitHub加速"
date: 2024-11-04T12:34:25+08:00
lastmod: 2024-11-04T22:54:22+08:00
draft: false
math: true
categories:
- 教程
tags:
- GitHub
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


# GitHub加速访问

# GitHub520

https://github.com/521xueweihan/GitHub520

😘 让你“爱”上 GitHub，解决访问时图裂、加载慢的问题。

## 一、介绍

对 GitHub 说"爱"太难了：访问慢、图片加载不出来。

**本项目无需安装任何程序，仅需 5 分钟。**

通过修改本地 hosts 文件，试图解决：

- GitHub 访问速度慢的问题
- GitHub 项目中的图片显示不出的问题

让你"爱"上 GitHub。

_注：_ 本项目还处于测试阶段，仅在本机测试通过，如有问题欢迎提 [issues](https://github.com/521xueweihan/GitHub520/issues/new)

## 二、使用方法

下面的地址无需访问 GitHub 即可获取到最新的 hosts 内容：

- 文件：`https://raw.hellogithub.com/hosts`
- JSON：`https://raw.hellogithub.com/hosts.json`

### 2.1 手动方式

#### 2.1.1 复制下面的内容


```shell
# GitHub520 Host Start
140.82.112.26                 alive.github.com
140.82.113.6                  api.github.com
185.199.109.153               assets-cdn.github.com
185.199.108.133               avatars.githubusercontent.com
185.199.108.133               avatars0.githubusercontent.com
185.199.111.133               avatars1.githubusercontent.com
185.199.111.133               avatars2.githubusercontent.com
185.199.108.133               avatars3.githubusercontent.com
185.199.111.133               avatars4.githubusercontent.com
185.199.108.133               avatars5.githubusercontent.com
185.199.108.133               camo.githubusercontent.com
140.82.113.21                 central.github.com
185.199.111.133               cloud.githubusercontent.com
140.82.113.10                 codeload.github.com
140.82.114.21                 collector.github.com
185.199.111.133               desktop.githubusercontent.com
185.199.111.133               favicons.githubusercontent.com
140.82.112.3                  gist.github.com
3.5.30.3                      github-cloud.s3.amazonaws.com
54.231.168.153                github-com.s3.amazonaws.com
52.217.194.73                 github-production-release-asset-2e65be.s3.amazonaws.com
52.217.191.25                 github-production-repository-file-5c1aeb.s3.amazonaws.com
54.231.230.209                github-production-user-asset-6210df.s3.amazonaws.com
192.0.66.2                    github.blog
140.82.112.3                  github.com
140.82.112.18                 github.community
185.199.110.154               github.githubassets.com
151.101.193.194               github.global.ssl.fastly.net
185.199.110.153               github.io
185.199.111.133               github.map.fastly.net
185.199.109.153               githubstatus.com
140.82.114.25                 live.github.com
185.199.111.133               media.githubusercontent.com
185.199.108.133               objects.githubusercontent.com
13.107.42.16                  pipelines.actions.githubusercontent.com
185.199.111.133               raw.githubusercontent.com
185.199.111.133               user-images.githubusercontent.com
140.82.113.21                 education.github.com
185.199.111.133               private-user-images.githubusercontent.com


# Update time: 2024-11-04T10:30:30+08:00
# Update url: https://raw.hellogithub.com/hosts
# Star me: https://github.com/521xueweihan/GitHub520
# GitHub520 Host End

```

该内容会自动定时更新， 数据更新时间：2024-11-04T10:30:30+08:00

#### 2.1.2 修改 hosts 文件

hosts 文件在每个系统的位置不一，详情如下：

- Windows 系统：`C:\Windows\System32\drivers\etc\hosts`
- Linux 系统：`/etc/hosts`
- Mac（苹果电脑）系统：`/etc/hosts`
- Android（安卓）系统：`/system/etc/hosts`
- iPhone（iOS）系统：`/etc/hosts`

修改方法，把第一步的内容复制到文本末尾：

1. Windows 使用记事本。
2. Linux、Mac 使用 Root 权限：`sudo vi /etc/hosts`。
3. iPhone、iPad 须越狱、Android 必须要 root。

#### 2.1.3 激活生效

大部分情况下是直接生效，如未生效可尝试下面的办法，刷新 DNS：

1. Windows：在 CMD 窗口输入：`ipconfig /flushdns`
    
2. Linux 命令：`sudo nscd restart`，如报错则须安装：`sudo apt install nscd` 或 `sudo /etc/init.d/nscd restart`
    
3. Mac 命令：`sudo killall -HUP mDNSResponder`
    

**Tips：** 上述方法无效可以尝试重启机器。

### 2.2 自动方式（SwitchHosts）

**Tip**：推荐 [SwitchHosts](https://github.com/oldj/SwitchHosts) 工具管理 hosts

以 SwitchHosts 为例，看一下怎么使用的，配置参考下面：

- Hosts 类型: `Remote`
- Hosts 标题: 随意
- URL: `https://raw.hellogithub.com/hosts`
- 自动刷新: 最好选 `1 小时`


如图：

[![](https://github.com/521xueweihan/GitHub520/raw/main/img/switch-hosts.png)](https://github.com/521xueweihan/GitHub520/blob/main/img/switch-hosts.png)

这样每次 hosts 有更新都能及时进行更新，免去手动更新。

### 2.3 一行命令

#### Windows

使用命令需要安装[git bash](https://gitforwindows.org/) 复制以下命令保存到本地命名为**fetch_github_hosts**

```shell
_hosts=$(mktemp /tmp/hostsXXX)
hosts=/c/Windows/System32/drivers/etc/hosts
remote=https://raw.hellogithub.com/hosts
reg='/# GitHub520 Host Start/,/# Github520 Host End/d'

sed "$reg" $hosts > "$_hosts"
curl "$remote" >> "$_hosts"
cat "$_hosts" > "$hosts"

rm "$_hosts"
```

在**CMD**中执行以下命令，执行前需要替换**git-bash.exe**和**fetch_github_hosts**为你本地的路径，注意前者为windows路径格式后者为shell路径格式

`"C:\Program Files\Git\git-bash.exe" -c "/c/Users/XXX/fetch_github_hosts"`

可以将上述命令添加到windows的task schedular（任务计划程序）中以定时执行

#### GNU（Ubuntu/CentOS/Fedora）

`sudo sh -c 'sed -i "/# GitHub520 Host Start/Q" /etc/hosts && curl https://raw.hellogithub.com/hosts >> /etc/hosts'`

#### BSD/macOS

`sudo sed -i "" "/# GitHub520 Host Start/,/# Github520 Host End/d" /etc/hosts && curl https://raw.hellogithub.com/hosts | sudo tee -a /etc/hosts`

将上面的命令添加到 cron，可定时执行。使用前确保 GitHub520 内容在该文件最后部分。

**在 Docker 中运行，若遇到 `Device or resource busy` 错误，可使用以下命令执行**

`cp /etc/hosts ~/hosts.new && sed -i "/# GitHub520 Host Start/Q" ~/hosts.new && curl https://raw.hellogithub.com/hosts >> ~/hosts.new && cp -f ~/hosts.new /etc/hosts`

### 2.4 AdGuard 用户（自动方式）

在 **过滤器>DNS 封锁清单>添加阻止列表>添加一个自定义列表**，配置如下：

- 名称：随意
- URL：`https://raw.hellogithub.com/hosts`（和上面 SwitchHosts 使用的一样）

如图：

[![](https://github.com/521xueweihan/GitHub520/raw/main/img/AdGuard-rules.png)](https://github.com/521xueweihan/GitHub520/blob/main/img/AdGuard-rules.png)

更新间隔在 **设置 > 常规设置 > 过滤器更新间隔（设置一小时一次即可）**，记得勾选上 **使用过滤器和 Hosts 文件以拦截指定域名**

[![](https://github.com/521xueweihan/GitHub520/raw/main/img/AdGuard-rules2.png)](https://github.com/521xueweihan/GitHub520/blob/main/img/AdGuard-rules2.png)

**Tip**：不要添加在 **DNS 允许清单** 内，只能添加在 **DNS 封锁清单** 才管用。 另外，AdGuard for Mac、AdGuard for Windows、AdGuard for Android、AdGuard for IOS 等等 **AdGuard 家族软件** 添加方法均类似。

## 三、效果对比

之前的样子：

[![](https://github.com/521xueweihan/GitHub520/raw/main/img/old.png)](https://github.com/521xueweihan/GitHub520/blob/main/img/old.png)

修改完 hosts 的样子：

[![](https://github.com/521xueweihan/GitHub520/raw/main/img/new.png)](https://github.com/521xueweihan/GitHub520/blob/main/img/new.png)

## TODO


- [x]  定时自动更新 hosts 内容
- [x]  hosts 内容无变动不会更新
- [x]  寻到最优 IP 解析结果

## 声明

[![知识共享许可协议](https://camo.githubusercontent.com/4fd85df1f1211fcfcd64c807ab0d6c3dc2eed34261ad65bd33e6d6eff306ab1f/68747470733a2f2f6c6963656e7365627574746f6e732e6e65742f6c2f62792d6e632d6e642f342e302f38387833312e706e67)](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh)  
本作品采用 [署名-非商业性使用-禁止演绎 4.0 国际](https://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh) 进行许可。



# SwitchHosts

https://github.com/oldj/SwitchHosts

- [简体中文](https://github.com/oldj/SwitchHosts/blob/master/README.zh_hans.md)
- [繁體中文](https://github.com/oldj/SwitchHosts/blob/master/README.zh_hant.md)

Homepage: [https://switchhosts.vercel.app](https://switchhosts.vercel.app/)

SwitchHosts is an App for managing hosts file, it is based on [Electron](http://electron.atom.io/) , [React](https://facebook.github.io/react/), [Jotai](https://jotai.org/) , [Chakra UI](https://chakra-ui.com/), [CodeMirror](http://codemirror.net/), etc.

## Screenshot

[![Capture](https://raw.githubusercontent.com/oldj/SwitchHosts/master/screenshots/sh_light.png)](https://raw.githubusercontent.com/oldj/SwitchHosts/master/screenshots/sh_light.png)

## Features

- Switch hosts quickly
- Syntax highlight
- Remote hosts
- Switch from system tray

## Install

### Download

You can download the source code and build it yourself, or download the built version from following links:

- [SwitchHosts Download Page (GitHub release)](https://github.com/oldj/SwitchHosts/releases)

You can also install the built version using the [package manager Chocolatey](https://community.chocolatey.org/packages/switchhosts):

```powershell
choco install switchhosts
```

## Backup

SwitchHosts stores data at `~/.SwitchHosts` (Or folder `.SwitchHosts` under the current user's home path on Windows), the `~/.SwitchHosts/data` folder contains data, while the `~/.SwitchHosts/config` folder contains various configuration information.

## Develop and build

### Development

- Install [Node.js](https://nodejs.org/)
- Change to the folder `./`, run `npm install` to install dependented libraries
- Run `npm run dev` to start the development server
- Then run `npm run start` to start the app for developing or debuging

### Build and package

- It is recommended to use [electron-builder](https://github.com/electron-userland/electron-builder) for packaging
- Go to the `./` folder
- Run `npm run build`
- Run `npm run make`, if everything goes well, the packaged files will be in the `./dist` folder.
- This command may take several minutes to finish when you run it the first time, as it needs time to download dependent files. You can download the dependencies manually [here](https://github.com/electron/electron/releases), or [Taobao mirror](https://npmmirror.com/mirrors/electron/), then save the files to `~/.electron` . You can check the [Electron Docs](http://electron.atom.io/docs/) for more infomation.

```shell
# build
npm run build

# make
npm run make # the packed files will be in ./dist
```

## Copyright

SwitchHosts is a free and open source software, it is released under the [Apache License](https://github.com/oldj/SwitchHosts/blob/master/LICENSE).



# 如何修改hosts文件？几种修改hosts文件的方法

https://zhuanlan.zhihu.com/p/438447914

最简单方式：将hosts文件复制到桌面，然后使用记事本编辑，修改完成后，再替换掉系统盘的hosts文件，这样可以解决Win10 修改不了hosts文件的问题。




