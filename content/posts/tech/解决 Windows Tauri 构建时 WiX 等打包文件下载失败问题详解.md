---
title: "解决 Windows Tauri 构建时 WiX 等打包文件下载失败问题详解"
date: 2024-06-14T18:34:25+08:00
lastmod: 2024-06-14T22:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- Windows
- Tauri
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

# 解决 Windows Tauri 构建时 WiX 等打包文件下载失败问题详解


## 前言

在使用 Tauri 进行 Windows 应用构建时，经常会遇到 WiX、NSIS 等必需的打包工具及插件下载失败，导致构建过程超时或失败的情况。尤其是在有全局翻墙需求的环境中更为常见。本文总结了手动下载和配置这些依赖的方法，并附上实验验证的操作步骤，帮助大家顺利完成构建。

---

## 1. 问题背景与目录结构要求

当构建 Windows Tauri 应用时，如果网络环境导致依赖文件无法自动下载，构建过程会报错、超时或者失败。针对常见的依赖包：

- `wix311-binaries.zip`（WiX 工具集）
- `nsis-3.zip`（NSIS 安装包工具）
- NSIS 插件 `ApplicationID.dll`、`nsis_tauri_utils.dll`

需要**手动下载并放置在特定目录**，且**目录名和文件路径大小写需严格匹配**，否则会导致后续构建检测失败。

---

## 2. 手动下载及部署步骤

### 2.1 WiX工具包

- 手动下载 WiX工具包：
    
    > [WiX 3.11 二进制文件下载链接](https://github.com/wixtoolset/wix3/releases/download/wix3112rtm/wix311-binaries.zip)
    
- 解压后，创建文件夹：
    
    ```
    C:\Users\你的用户名\AppData\Local\tauri\WixTools
    ```
    
- 将解压后的所有 WiX 文件复制到 `WixTools` 文件夹。
    

> **注意：** 如果你下载的是 WiX 3.14 版本，相应文件夹需命名为 `WixTools314`，经实测该名称可行。

### 2.2 NSIS 安装工具

- 下载 NSIS 压缩包：
    
    > [NSIS 3.x.zip 下载链接](https://github.com/tauri-apps/binary-releases/releases/download/nsis-3/nsis-3.zip)
    
- 解压后，新建文件夹：
    
    ```
    C:\Users\你的用户名\AppData\Local\tauri\NSIS
    ```
    
- 将解压后的 NSIS 文件全部复制到 `NSIS` 文件夹。
    

### 2.3 NSIS 插件文件

NSIS 目录中的插件文件夹缺少两个关键插件文件，需单独下载：

- **ApplicationID插件**
    
    > [NSIS-ApplicationID.zip](https://github.com/tauri-apps/binary-releases/releases/download/nsis-plugins-v0/NSIS-ApplicationID.zip)
    
- **nsis_tauri_utils.dll**
    
    > [nsis_tauri_utils.dll 下载链接](https://github.com/tauri-apps/nsis-tauri-utils/releases/download/nsis_tauri_utils-v0.1.1/nsis_tauri_utils.dll)
    

解压 `NSIS-ApplicationID.zip` 后，将内容复制到：

```
C:\Users\你的用户名\AppData\Local\tauri\NSIS\Plugins\x86-unicode\
```

同时，将下载的 `nsis_tauri_utils.dll` 文件也放入上述路径。

---

## 3. 目录整体结构示例

以 `C:\Users\用户名\AppData\Local\tauri\` 目录为例，整体文件夹应如下：

```
tauri
├─WixTools
│   └─（WiX工具包解压文件）
│
└─NSIS
    ├─Bin
    ├─Contrib
    ├─Docs
    ├─Examples
    ├─Include
    ├─Plugins
    │   ├─x86-ansi
    │   └─x86-unicode
    │       ├─ApplicationID.dll
    │       └─nsis_tauri_utils.dll
    └─Stubs
```

---

## 4. 原理及源码参考

Tauri 在构建过程中，会检测上述工具和插件文件是否存在。

主要源码检查位置：

- WiX 文件检测：
    
    [msi.rs#L28-L33](https://github.com/tauri-apps/tauri/blob/dev/tooling/bundler/src/bundle/windows/msi.rs#L28)  
    [wix.rs#L33](https://github.com/tauri-apps/tauri/blob/dev/tooling/bundler/src/bundle/windows/msi/wix.rs#L33)
    
- NSIS 文件检测：
    
    [nsis.rs#L47](https://github.com/tauri-apps/tauri/blob/dev/tooling/bundler/src/bundle/windows/nsis.rs#L47)
    

**关键点：** 如果程序发现必需文件不存在（包括插件文件），就会删除对应文件夹并尝试重新下载，导致下载失败且构建中断。
## 5. 总结

遇到 Windows 平台上 Tauri 构建时，因为网络问题导致自动下载 WiX 或 NSIS 失败时，可采用本文中的手动下载方案，将压缩包解压到指定路径，确保目录和文件结构完整无误。尤其要注意 NSIS 文件夹下缺失的插件文件，需单独手动下载并放置。

只要按照上述步骤操作，基本可以解决绝大多数 Tauri Windows 构建中打包文件下载失败的问题，保证构建流程顺畅。

## 参考资料

[如何解决安装失败](https://github.com/tauri-apps/tauri/issues/7338)

[解决windows Tauri 构建时下载 WiX等其它打包文件失败](https://blog.csdn.net/shiejiang8710/article/details/133579838)

## 附录 PowerShell 脚本

**环境验证通过 ✅**  
Tauri `v2.4.1` | WixTools `3.14` | NSIS `3` | nsis_tauri_utils `v0.4.2`

**使用说明：**

1. 保存为 `.ps1` 脚本执行
2. 自动清理旧数据 → **请提前备份**
3. 临时目录 `temp` 自动创建/删除

**若打包失败：**  
👉 检查下载版本是否匹配日志中的需求版本  
👉 修改脚本中的下载链接即可

**以下是脚本内容**

```powershell
# 1. 删除之前的临时目录和目标目录，保证干净环境
Remove-Item -Recurse -Force -ErrorAction SilentlyContinue temp
$tauriDir = Join-Path $env:USERPROFILE "AppData\Local\tauri"
Remove-Item -Recurse -Force -ErrorAction SilentlyContinue (Join-Path $tauriDir "NSIS")
Remove-Item -Recurse -Force -ErrorAction SilentlyContinue (Join-Path $tauriDir "WixTools314")

# 2. 创建临时目录
if (!(Test-Path temp)) { mkdir temp }
cd temp

# 3. 下载 wix 工具（WixTools314）
Invoke-WebRequest -Uri "https://github.com/wixtoolset/wix3/releases/download/wix3141rtm/wix314-binaries.zip" -OutFile "wix314-binaries.zip"
Expand-Archive ./wix314-binaries.zip -DestinationPath ./WixTools314

# 4. 下载 NSIS
Invoke-WebRequest -Uri "https://github.com/tauri-apps/binary-releases/releases/download/nsis-3/nsis-3.zip" -OutFile "nsis-3.zip"
Expand-Archive ./nsis-3.zip -DestinationPath ./NSIS

# 5. 移动 NSIS 文件夹下的 nsis-3.* 子目录内容到 NSIS 根目录
$nsisSubDir = Get-ChildItem .\NSIS | Where-Object { $_.PSIsContainer -and $_.Name -like 'nsis-3.*' } | Select-Object -First 1
if ($nsisSubDir) {
    Move-Item -Path (Join-Path $nsisSubDir.FullName '*') -Destination .\NSIS -Force
    Remove-Item $nsisSubDir.FullName -Recurse -Force
}

# 6. 下载 NSIS-ApplicationID 插件并解压
Invoke-WebRequest -Uri "https://github.com/tauri-apps/binary-releases/releases/download/nsis-plugins-v0/NSIS-ApplicationID.zip" -OutFile "NSIS-ApplicationID.zip"
Expand-Archive .\NSIS-ApplicationID.zip -DestinationPath .\NSIS-ApplicationID

# 7. 移动插件文件到 NSIS\Plugins\x86-unicode
$pluginDir = ".\NSIS\Plugins\x86-unicode"
if (!(Test-Path $pluginDir)) { New-Item -ItemType Directory -Path $pluginDir | Out-Null }
if (Test-Path ".\NSIS-ApplicationID\Release") {
    Move-Item ".\NSIS-ApplicationID\Release\*" $pluginDir -Force
}

# 8. 下载 nsis_tauri_utils.dll v0.4.2 并重命名覆盖到插件目录
Invoke-WebRequest -Uri "https://github.com/tauri-apps/nsis-tauri-utils/releases/download/nsis_tauri_utils-v0.4.2/nsis_tauri_utils.dll" -OutFile "nsis_tauri_utils.dll"
if (Test-Path "nsis_tauri_utils.dll") {
    Move-Item "nsis_tauri_utils.dll" (Join-Path $pluginDir "nsis_tauri_utils.dll") -Force
}

# 9. 移动 NSIS 和 WixTools314 到用户目录
if (!(Test-Path $tauriDir)) { New-Item -ItemType Directory -Path $tauriDir | Out-Null }
Move-Item .\NSIS (Join-Path $tauriDir "NSIS") -Force -ErrorAction SilentlyContinue
Move-Item .\WixTools314 (Join-Path $tauriDir "WixTools314") -Force -ErrorAction SilentlyContinue

Write-Host "rm temp dir"

# 10. 清理临时文件和目录
Remove-Item .\NSIS-ApplicationID -Recurse -Force -ErrorAction SilentlyContinue
Remove-Item .\nsis-3.zip -Force -ErrorAction SilentlyContinue
Remove-Item .\NSIS-ApplicationID.zip -Force -ErrorAction SilentlyContinue
Remove-Item .\wix314-binaries.zip -Force -ErrorAction SilentlyContinue
cd ..
Remove-Item .\temp -Recurse -Force -ErrorAction SilentlyContinue

Write-Host "done"
```



















