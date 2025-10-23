---
title: "解除捆绑：轻松卸载 Windows 11 预装应用全攻略"
date: 2025-06-02T22:34:25+08:00
lastmod: 2025-06-03T22:54:22+08:00
math: true
categories:
- 生活
tags:
- Windows
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

# 解除捆绑：轻松卸载 Windows 11 预装应用全攻略

## 前言

Windows 11 默认预装了不少微软的自带应用，但其中许多应用可能你根本用不上，占用系统资源和存储空间。本文将详细介绍如何利用 PowerShell 快速、安全地卸载这些捆绑应用，帮助你打造更简洁高效的系统环境。

---

## 一、准备工作：打开 PowerShell

卸载预装应用需要管理员权限操作，请按照以下步骤打开 PowerShell：

1. **右键点击「开始」菜单图标**，选择【终端管理员】打开 Windows 终端。
2. 按下快捷键 `Ctrl + Shift + 1`，切换到 Windows PowerShell 窗口。
3. 使用以下命令模板卸载指定应用（仅影响当前用户）：
    
    ```powershell
    Get-AppxPackage <Package_Name> -User $env:UserName | Remove-AppxPackage
    ```
    

---

## 二、常见可直接卸载的预装应用

不同版本的 Windows 11（如 23H2、24H2）预装的应用略有差异，下面列举一些常见且适合卸载的应用及其卸载命令。

### 1. 纸牌游戏（Solitaire & Casual Games）

经典纸牌游戏被广告侵占且视觉设计花哨，如果你不玩，建议卸载以释放系统资源。

```powershell
Get-AppxPackage Microsoft.MicrosoftSolitaireCollection -User $env:UserName | Remove-AppxPackage
```

### 2. Cortana

微软已经极大削减了 Cortana 的服务功能，实用性大不如前，无需继续保留。

```powershell
Get-AppxPackage Microsoft.549981C3F5F10 -User $env:UserName | Remove-AppxPackage
```

### 3. 邮件和日历

随着新版 Outlook for Windows 推出，原生的邮件和日历应用将被替代，建议卸载。

```powershell
Get-AppxPackage Microsoft.WindowsCommunicationsApps -User $env:UserName | Remove-AppxPackage
```

### 4. 相机

大部分 PC 用户几乎不用内置的相机应用，除非你是 Surface Pro 等设备用户，一般可以卸载。

```powershell
Get-AppxPackage Microsoft.WindowsCamera -User $env:UserName | Remove-AppxPackage
```

### 5. 资讯（Microsoft Start新闻）

资讯应用内容多为点击诱饵，实用价值低，建议卸载。

```powershell
Get-AppxPackage Microsoft.BingNews -User $env:UserName | Remove-AppxPackage
```

### 6. 地图

由于 Windows Phone 已停服，地图应用对多数用户意义不大。移动端地图应用如高德、百度、腾讯更适合使用。

```powershell
Get-AppxPackage Microsoft.WindowsMaps -User $env:UserName | Remove-AppxPackage
```

### 7. Microsoft 365 门户

这只是 PWA 形式的入口，如需使用直接访问官网即可，无需占用本地资源。

```powershell
Get-AppxPackage Microsoft.MicrosoftOfficeHub -User $env:UserName | Remove-AppxPackage
```

---

## 三、按需卸载的应用

以下应用功能较为专业或场景有限，用户可根据需求选择保留或卸载。

### 1. Clipchamp（视频编辑）

微软的视频编辑工具，功能强大类似苹果 iMovie，不剪辑视频可卸载。

```powershell
Get-AppxPackage Clipchamp.Clipchamp -User $env:UserName | Remove-AppxPackage
```

### 2. Microsoft Teams

集成了聊天、视频会议、文件管理，非办公场景用户可选择卸载。

```powershell
Get-AppxPackage MSTeams -User $env:UserName | Remove-AppxPackage
```

### 3. Dev Home（开发人员主页）

为开发者设计的控制中心，支持定制和环境搭建，不是开发者可卸载。

```powershell
Get-AppxPackage Microsoft.Windows.DevHome -User $env:UserName | Remove-AppxPackage
```

### 4. 录音机

适合简单录音，若需求专业可用 Audacity 等第三方软件替代。

```powershell
Get-AppxPackage Microsoft.WindowsSoundRecorder -User $env:UserName | Remove-AppxPackage
```

### 5. 天气

卸载后无法锁屏查看天气，但小组件天气信息不受影响。

```powershell
Get-AppxPackage Microsoft.BingWeather -User $env:UserName | Remove-AppxPackage
```

### 6. 便笺

轻量级在线同步笔记工具，不常用或习惯用更强大的如 OneNote、Notion 可卸载。

```powershell
Get-AppxPackage Microsoft.MicrosoftStickyNotes -User $env:UserName | Remove-AppxPackage
```

---

## 四、卸载注意事项

- **仅当前用户生效**：卸载命令默认只针对当前登录账户生效。
- **操作需谨慎**：建议事先备份重要数据，避免误删系统关键组件。
- **版本差异**：不同 Windows 11 版本可能预装应用稍有不同，需要根据具体系统版本调整。
- **恢复应用**：可通过 Microsoft Store 重新安装已卸载应用。

---

## 五、总结

合理卸载不需要的预装应用，可以释放系统资源，提升 Windows 11 的运行效率和使用体验。根据个人使用习惯，选择性卸载最适合你的应用，打造干净、高效的操作环境。


# 附录批量处理脚本

下面是一个简单的 PowerShell 批量卸载脚本模板，你可以根据需要修改其中的应用包名，运行时会逐条执行卸载命令，仅影响当前用户：

```powershell
# 批量卸载 Windows 11 预装应用脚本

# 定义需要卸载的应用包名列表
$appPackages = @(
    "Microsoft.MicrosoftSolitaireCollection",  # 纸牌游戏
    "Microsoft.549981C3F5F10",                  # Cortana
    "Microsoft.WindowsCommunicationsApps",      # 邮件和日历
    "Microsoft.WindowsCamera",                   # 相机
    "Microsoft.BingNews",                        # 资讯应用
    "Microsoft.WindowsMaps",                     # 地图
    "Microsoft.MicrosoftOfficeHub",              # Microsoft 365 门户
    "Clipchamp.Clipchamp",                       # Clipchamp 视频编辑
    "MSTeams",                                  # Microsoft Teams
    "Microsoft.Windows.DevHome",                 # Dev Home 开发者主页
    "Microsoft.WindowsSoundRecorder",            # 录音机
    "Microsoft.BingWeather",                      # 天气
    "Microsoft.MicrosoftStickyNotes"              # 便笺应用
)

# 遍历卸载
foreach ($package in $appPackages) {
    Write-Host "正在卸载 $package ..."
    Get-AppxPackage $package -User $env:UserName | Remove-AppxPackage -ErrorAction SilentlyContinue
}

Write-Host "卸载完成！"
```

**使用方法：**

1. 以管理员身份打开 Windows 终端并切换到 PowerShell。
2. 将上述代码复制粘贴到终端中执行即可。

如果你只想卸载部分应用，把不需要卸载的包名从 `$appPackages` 数组中删除即可。

需要注意，系统关键组件及一些预装应用可能无法卸载，脚本会自动忽略报错，保持执行流程畅通。

更完整版本的批处理文件如下所示：

```bat
@echo =========================================
@echo 1.Uninstall OneDrive
@echo Uninstall OneDrive for win11
@echo -------------------------------------------------------------
%SYSTEMROOT%\SysWOW64\OneDriveSetup.exe /uninstall /q
%SYSTEMROOT%\System32\OneDriveSetup.exe /uninstall /q

@echo =========================================
@echo 2.Uninstall Appx for the current user
@echo Remove-AppxPackage cmdlet removes an app package from a user account.
@echo -------------------------------------------------------------
PowerShell "Get-AppxPackage *Clipchamp* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.549981C3F5F10* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.BingNews* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.BingWeather* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.GamingApp* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.GetHelp* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.Getstarted* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.Microsoft3DViewer* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.MicrosoftOfficeHub* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.MicrosoftSolitaireCollection* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.MicrosoftStickyNotes* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.MixedReality.Portal* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.MSPaint* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.Office.OneNote* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.People* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.PowerAutomateDesktop* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.ScreenSketch* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.SkypeApp* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.Todos* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.WindowsFeedbackHub* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.WindowsMaps* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.Xbox* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *Microsoft.YourPhone* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *MicrosoftCorporationII.QuickAssist* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *MicrosoftTeams* -AllUsers | Remove-AppxPackage"
PowerShell "Get-AppxPackage *MicrosoftWindows.Client.WebExperience* -AllUsers | Remove-AppxPackage"
REM PowerShell "Get-AppxPackage -AllUsers | Remove-AppxPackage"

@echo =========================================
@echo 3.Uninstall Appx from the computer for all users
@echo The Remove-AppxProvisionedPackage cmdlet removes app packages (.appx) from a Windows image.
@echo App packages will not be installed when new user accounts are created.
@echo Packages will not be removed from existing user accounts.
@echo To remove app packages (.appx) that are not provisioned or to remove a package for a particular user only, use Remove-AppxPackage instead.
@echo -------------------------------------------------------------
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Clipchamp*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.549981C3F5F10*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.BingNews*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.BingWeather*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.GamingApp*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.GetHelp*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.Getstarted*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.Microsoft3DViewer*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.MicrosoftOfficeHub*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.MicrosoftSolitaireCollection*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.MicrosoftStickyNotes*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.MixedReality.Portal*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.MSPaint*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.Office.OneNote*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.People*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.PowerAutomateDesktop*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.ScreenSketch*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.SkypeApp*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.Todos*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.WindowsFeedbackHub*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.WindowsMaps*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.Xbox*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*Microsoft.YourPhone*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*MicrosoftCorporationII.QuickAssist*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*MicrosoftTeams*\"} | Remove-AppxProvisionedPackage -Online"
PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -like \"*MicrosoftWindows.Client.WebExperience*\"} | Remove-AppxProvisionedPackage -Online"
REM PowerShell "Get-AppxProvisionedPackage -Online | Where-Object {$_.packagename -unlike \"store\"} | Remove-AppxProvisionedPackage -Online"
```
# 参考资料

[解除捆绑：如何轻松卸载 Windows 11 预装应用](https://www.sysgeek.cn/remove-bundled-apps-windows/)

[处理一键删除Win10/Win11预装程序Appx](https://zhuanlan.zhihu.com/p/606606682)









