---
title: "Windows 11 上配置多个 GitHub 账号的完整指南"
date: 2025-05-26T21:34:25+08:00
lastmod: 2025-05-26T21:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- Windows
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


# Windows 11 上配置多个 GitHub 账号的完整指南

## 0. 前言

你是否和我一样，有两个 GitHub 账号？一个用于协作团队项目，另一个用于个人创作。想让它们在本地和远端完全隔离，互不干扰？

问题是，Git 默认用全局 `user.name` 和 `user.email`，这会让提交记录看起来混淆身份。更复杂的是，SSH 密钥是权限的关键，每个密钥只能归属于一个账号。电脑默认使用一个 SSH key 连接 github.com，也导致只能无密码访问其中一个账号。

本文将一步步教你在 Windows 11 中：

- 如何为不同账号生成独立 SSH 密钥
- 如何配置 SSH 客户端自动识别不同密钥
- 如何按仓库设置对应的用户信息
- 如何使用自定义 SSH Host 访问不同账号仓库

---

## 1. 生成多个 SSH 密钥

打开命令行（Windows Terminal 或 Git Bash），切换到 `.ssh` 文件夹：

```bash
cd %USERPROFILE%\.ssh
```

生成第一个账号的密钥：

```bash
ssh-keygen -t rsa -b 4096 -C "account1_email@example.com" -f id_rsa_account1
```

生成第二个账号的密钥（注意 `-f` 参数自定义文件名，避免覆盖）：

```bash
ssh-keygen -t rsa -b 4096 -C "account2_email@example.com" -f id_rsa_account2
```

这会生成两对密钥文件：

- `id_rsa_account1` 和 `id_rsa_account1.pub`
- `id_rsa_account2` 和 `id_rsa_account2.pub`

---

## 2. 将公钥添加到对应的 GitHub 账号

分别登录两个 GitHub 账号，进入：  
**Settings → SSH and GPG keys → New SSH key**

将对应 `.pub` 文件内容复制粘贴进去，保存。

> 添加后，可以用下面命令测试 SSH 连接是否生效（注意路径替换成自己的绝对路径）：

```bash
ssh -T -i ~/.ssh/id_rsa_account1 git@github.com
ssh -T -i ~/.ssh/id_rsa_account2 git@github.com
```

如果看到

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

则说明配置无误。

---

## 3. 配置 SSH 客户端 config 文件

新建或编辑 `%USERPROFILE%\.ssh\config` 文件，添加如下内容：

```text
# Account 1
Host github-account1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_account1
    IdentitiesOnly yes

# Account 2
Host github-account2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_account2
    IdentitiesOnly yes
```

这里定义了两个“主机别名”：

- `github-account1` 使用账户 1 的私钥
- `github-account2` 使用账户 2 的私钥

`IdentitiesOnly yes` 确保 SSH 只用这里指定的 key。

---

## 4. 克隆和操作仓库时使用自定义 Host

更改仓库的远程地址，把默认的 `github.com` 替换成对应的自定义 Host：

- 账号 1 的仓库地址示例：
    
    ```
    git clone git@github-account1:username1/repo.git
    ```
    
- 账号 2 的仓库地址示例：
    
    ```
    git clone git@github-account2:username2/repo.git
    ```
    

如果是已经存在的仓库，可以进入项目目录修改远程地址：

```bash
git remote set-url origin git@github-account1:username1/repo.git
```

这样操作时，Git 会自动调用对应的 SSH 密钥，实现账号归属分明。

---

## 5. 配置本地仓库的用户名和邮箱

建议不要设置全局的 `user.name` 和 `user.email`，改为在每个仓库单独配置：

先取消全局配置：

```bash
git config --global --unset user.name
git config --global --unset user.email
```

进入不同仓库目录，设置对应的身份：

```bash
git config user.name "Your Name - Account 1"
git config user.email "account1_email@example.com"
```

或者

```bash
git config user.name "Your Name - Account 2"
git config user.email "account2_email@example.com"
```

你可以使用以下命令查看配置：

```bash
git config user.name
git config user.email
```

确认是当前仓库的本地设置，不会影响其他仓库。

---

## 6. 额外提示和总结

- **不要用同一对 SSH key 关联多个 GitHub 账号**，GitHub 会限制并且 SSH 客户端不会自动切换。
- `~/.ssh/config` 文件配置正确，能让你在一台电脑上无缝操作多个账号。
- 记住，远程仓库地址里的 Host 名称要和 `config` 中的对应。
- 始终为每个仓库单独设置用户信息，避免身份混淆。

---


## 7. 通过.bat文件实现手动切换全局配置

下面这个简单的批处理脚本可以让用户输入账户名，然后根据不同的账户名设置对应的全局配置。例如：

```batch
@echo off
setlocal

:: 提示输入账户名称
set /p account=请输入账户名（比如：Account1 或 Account2）:

:: 先清除已有的 user.name 和 user.email
git config --global --unset user.name
git config --global --unset user.email

:: 根据不同账户设置
if /i "%account%"=="Account1" (
    git config --global user.name "你的账户1名字"
    git config --global user.email "youraccount1@example.com"
) else if /i "%account%"=="Account2" (
    git config --global user.name "你的账户2名字"
    git config --global user.email "youraccount2@example.com"
) else (
    echo 未识别的账户名，请确保输入正确。
)

pause
endlocal
```

这样运行脚本后，你会看到提示输入账户名，然后它会根据你的输入设置对应的全局git配置。你可以根据需要调整账户名和邮箱。
## 参考资料和链接

- [GitHub 官方 SSH 文档](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [Win11 配置多个 GitHub 账号](https://www.chengxulvtu.net/how-to-work-with-multiple-github-accounts-on-win11/)
- [Git 配置教程](https://git-scm.com/book/zh/v2/)

---

# 总结

通过以上步骤，在 Windows 11 电脑上配置并使用多个 GitHub 账号，既能保证远程访问权限独立，又能保证提交历史中的身份信息清晰准确。多账号管理不再混乱，代码协作更高效。




