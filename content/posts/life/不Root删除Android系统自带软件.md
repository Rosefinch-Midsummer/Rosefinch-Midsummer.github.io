---
title: "不Root删除Android系统自带软件"
date: 2023-11-11T18:34:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
categories:
- Android
tags:
- Android
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

# adb工具下载及环境配置（一看就会）

[文章来源](https://zhuanlan.zhihu.com/p/653371171)

### 1、adb工具下载

官网下载地址：[SDK 平台工具版本说明 | Android 开发者 | Android Developers](https://link.zhihu.com/?target=https%3A//developer.android.google.cn/studio/releases/platform-tools%3Fhl%3Dzh-cn)，选择想要安装的系统的哦！

![](https://pic1.zhimg.com/80/v2-be4ef22250904ebbf03c75635797ae0c_1440w.webp)

点击下载链接，勾选我已阅读并同意上述条款及条件并立即下载。将下载后的压缩包解压到指定目录，并来到这个目录下。

![](https://pic1.zhimg.com/80/v2-231570286d8af10740fa867efd5b1de8_1440w.webp)

拷贝该路径。

### 2、配置环境变量

右键此电脑，选择属性，点击高级系统设置。

![](https://pic2.zhimg.com/80/v2-974b78d736718a707587938363b614e9_1440w.webp)

点击环境变量。

![](https://pic3.zhimg.com/80/v2-8e92501db44b0927f148201b2db8497e_1440w.webp)

找到系统变量中的Path并双击。

![](https://pic1.zhimg.com/80/v2-bee83c2bce767c207c3a150225ebebec_1440w.webp)

点击新建，将之前复制的路径粘贴过来。

![](https://pic4.zhimg.com/80/v2-467970a7563147950bd2da6a049b89b3_1440w.webp)

然后连着点击三个确定。

### 3、验证adb环境变量添加是否成功

按住 win +R 键，输入cmd并点击确定，进入windows命令行窗口。

![](https://pic1.zhimg.com/80/v2-9cfa094177d5c2cc7496bce513bef15c_1440w.webp)

输入adb并按回车。

![](https://pic1.zhimg.com/80/v2-0c543f6e7949acfd97f257ea1e145150_1440w.webp)

若出现版本号等相关信息，即为成功。

![](https://pic1.zhimg.com/80/v2-895d7a74a7bffaca40f9a2a123a6d6dc_1440w.webp)

若出现‘adb’不是内部或外部命令，也不是可运行的程序或批处理文件。 即为失败（我没有这个配图）。

失败的小伙伴不要伤心，重启一下电脑看看再来试试看看会不会有惊喜！


# 安卓手机卸载预装应用（用ADB所以免ROOT）

[原文链接](https://zhuanlan.zhihu.com/p/577812240)

- **该方法比较简单，也很通用，适合各种安卓手机。**
- **不需要root，使用adb命令行。其实就是写行代码（卸载命令是唯一得）。**
- **需要一台电脑，一台手机，一根数据线。**

**本文流程：**

![](https://pic2.zhimg.com/80/v2-b0728ec0e6078d55ba3b602191b5efb1_1440w.webp)

## **一、电脑部署**

[Android 调试桥 (adb)](https://developer.android.google.cn/tools/adb?hl=zh-cn)

Android 调试桥 (`adb`) 是一种功能多样的命令行工具，可让您与设备进行通信。`adb` 命令可用于执行各种设备操作，例如安装和调试应用。`adb` 提供对 Unix shell（可用来在设备上运行各种命令）的访问权限。它是一种客户端-服务器程序，包括以下三个组件：

- **客户端**：用于发送命令。客户端在开发机器上运行。您可以通过发出 `adb` 命令从命令行终端调用客户端。
- **守护程序 (adbd)**：用于在设备上运行命令。守护程序在每个设备上作为后台进程运行。
- **服务器**：用于管理客户端与守护程序之间的通信。服务器在开发机器上作为后台进程运行。

`adb` 包含在 Android SDK 平台工具软件包中。您可以使用 [SDK 管理器](https://developer.android.google.cn/studio/intro/update?hl=zh-cn#sdk-manager)下载此软件包，该管理器会将其安装在 `android_sdk/platform-tools/` 下。如果您需要独立的 Android SDK 平台工具软件包，请[点击此处进行下载](https://developer.android.google.cn/studio/releases/platform-tools?hl=zh-cn)。

如需了解如何通过 `adb` 连接设备以供使用，包括如何使用 Connection Assistant 来排查常见问题，请参阅[在硬件设备上运行应用](https://developer.android.google.cn/studio/run/device?hl=zh-cn)。

### adb 的工作原理

当您启动某个 `adb` 客户端时，该客户端会先检查是否有 `adb` 服务器进程已在运行。如果没有，它会启动服务器进程。服务器在启动后会与本地 TCP 端口 5037 绑定，并监听 `adb` 客户端发出的命令。

**注意**：所有 `adb` 客户端均使用端口 5037 与 `adb` 服务器通信。

然后，服务器会与所有正在运行的设备建立连接。它通过扫描 5555 到 5585 之间（该范围供前 16 个模拟器使用）的奇数号端口查找模拟器。服务器一旦发现 `adb` 守护程序 (adbd)，便会与相应的端口建立连接。

每个模拟器都使用一对按顺序排列的端口：一个用于控制台连接的偶数号端口，另一个用于 `adb` 连接的奇数号端口。例如：

模拟器 1，控制台：5554  
模拟器 1，`adb`：5555  
模拟器 2，控制台：5556  
模拟器 2，`adb`：5557  
依此类推。

如上所示，在端口 5555 处与 `adb` 连接的模拟器与控制台监听端口为 5554 的模拟器是同一个。

服务器与所有设备均建立连接后，您便可以使用 `adb` 命令访问这些设备。由于服务器管理与设备的连接，并处理来自多个 `adb` 客户端的命令，因此您可以从任意客户端或从某个脚本控制任意设备。

### 在设备上启用 adb 调试

如要在通过 USB 连接的设备上使用 adb，您必须在设备的系统设置中启用 **USB 调试**（位于**开发者选项**下）。在 Android 4.2（API 级别 17）及更高版本中，**开发者选项**屏幕默认处于隐藏状态。如需将其显示出来，请[启用开发者选项](https://developer.android.google.cn/studio/debug/dev-options?hl=zh-cn#enable)。

现在，您已经可以通过 USB 连接设备了。您可以通过从 `android_sdk/platform-tools/` 目录执行 `adb devices` 来验证设备是否已连接。如果已连接，您将看到设备名称以“设备”形式列出。

**注意**：当您连接搭载 Android 4.2.2（API 级别 17）或更高版本的设备时，系统会显示一个对话框，询问您是否接受允许通过此计算机进行调试的 RSA 密钥。这种安全机制可以保护用户设备，因为它可以确保用户只有在能够解锁设备并确认对话框的情况下才能执行 USB 调试和其他 adb 命令。

如需详细了解如何通过 USB 连接到设备，请参阅[在硬件设备上运行应用](https://developer.android.google.cn/studio/run/device?hl=zh-cn)。

### 安装应用

您可以使用 `adb` 的 `install` 命令在模拟器或连接的设备上安装 APK：

adb install path_to_apk

安装测试 APK 时，必须在 `install` 命令中使用 `-t` 选项。如需了解详情，请参阅 [`-t`](https://developer.android.google.cn/tools/adb?hl=zh-cn#-t-option)。

如需安装多个 APK，请使用 `install-multiple`。如果您从 Play 管理中心为应用下载适用于特定设备的所有 APK，并希望将这些 APK 安装在模拟器或实体设备上，这种做法非常有用。

若要详细了解如何创建可安装在模拟器/设备实例上的 APK 文件，请参阅[构建和运行您的应用](https://developer.android.google.cn/studio/run?hl=zh-cn)。

### 原作者的方式

**下载ADB文件和驱动文件。** 到这里下载就行：[adb工具包最新版](http://www.downcc.com/soft/21006.html)

这是个常见的三流网站，不是官方网站，不过东西好用就行了，也没有广告。下载后得到一个压缩包然后解压。

![](https://pic3.zhimg.com/80/v2-08692d196855db4fd4dbc4273600c17a_1440w.webp)

打开安装Adb 1.3就行，英文寡人看不懂。

![](https://pic3.zhimg.com/80/v2-983cc95be670c53ab624b316b67cb59a_1440w.webp)

安装完成后，再打开，**会显示准备安装 ADB和Fastboot。 输入Y，回车。**

然后对话框问你**要不要安装USB调试驱动。输入Y，回车。**

![](https://pic3.zhimg.com/80/v2-f9df0fefb7a59f2fb9591034234991ba_1440w.webp)

我安装了所以显示没有文件要复制。

**安装USB驱动得时候，会弹出SUB驱动安装程序，顺着下一步完成即可。**

![](https://pic2.zhimg.com/80/v2-741f07590747a1561435f426399526f9_1440w.webp)

![](https://pic3.zhimg.com/80/v2-b7f5644b0a6d3dca59dffe186f5b0ada_1440w.webp)

ADB、Fastboot、驱动都装完了。这样ADB环境部署完成。

电脑部署完毕。

## **二、手机部署**

注：这里要根据自己手机型号确定打开“开发者模式”的方式。

**打开手机开发者模式：到设置--关于手机--版本号（不是安卓版本号，是厂商手机版本号，就写个版本号），连续点击版本号N次。最终显示：您已处于开发者模式。**

![](https://pic2.zhimg.com/80/v2-db891a83d3e4602e8442159fa1a7cab5_1440w.webp)

连续点击版本号

然后返回关于手机，里面多了一个选项：开发者模式。点击进来。往下找找，有一个 **USB调试 ，**打开他。

![](https://pic2.zhimg.com/80/v2-63d1717f2298f7d63e4b035e417d7969_1440w.webp)

手机部署完毕。

## **三、连接手机**

**按下win+R 组合键。输入cmd 回车。（打开了cmd命令行窗口）**

**把手机用手机选连接在电脑上。手机屏幕显示：是否允许调试，选择始终允许后再确定。如果不出来，可以试试下一步。**

![](https://pic2.zhimg.com/80/v2-161c3ff341db41a43b96ef555cbd33b5_1440w.webp)

**随后在CMD窗口里输入 adb devices**（下面代码方便直接复制）

```text
adb devices
```

此时会显示你的手机型号。大概是下面的样子，表示连接成功。

![](https://pic1.zhimg.com/80/v2-c56076847d77fefcb98ebbc59b27c6bc_1440w.webp)

**链接完毕。**

## **四、查看想卸载软件得包名**

[蓝奏云——包名查看器](https://www.lanzouj.com/i9hjvfg)

[52pojie-软件包名查看器介绍](https://www.52pojie.cn/thread-1110215-1-1.html)

建议搭配这个食用：[https://www.52pojie.cn/thread-1093838-1-1.html](https://www.52pojie.cn/thread-1093838-1-1.html)  

手机安装之后可以查看手机内所有软件的包名（包括系统软件），搭配上面的免root手机卸载工具，从而可以实现分类卸载。  

卸载之前建议仔细仔细再仔细！！！  

看不懂的包名就别卸载了，防止出现不能开机等问题。  

**比如同步助手得包名是 com.duoqin.syncassistant**

![](https://pic1.zhimg.com/80/v2-4faadcdf037b76e67e8d7ebe50f5f060_1440w.webp)

**学会查看包名。**

## **五、卸载软件**

在cmd里输入 **adb shell pm uninstall --user 0 + 包名**（注意没有＋号，看下图） 就卸载了软件，比如卸载同步助手（下图我卸载了3个，第三个我包名输入错误2次，所以失败2次。第三次成功了，就是白色那部分）

```text
adb shell pm uninstall --user 0
```

![](https://pic3.zhimg.com/80/v2-0b333b86570e5533b0c2f5d54351ab12_1440w.webp)

现在学会了卸载。

## 六、注意安全

有的东西看不懂就别卸载。比如你卸载个浏览器，那肯定没事。或者卸载个华为书城，也没事。但是有些东西不能卸载。**比如把华为视频卸载之后，华为手机就不能直接在相册里预览视频了。**

**我把上面的同步助手卸载了之后，我的手机有个遥控器功能，竟然不能用了**（下图）。提示我系统环境出错，就TM离谱，害我重新刷机刷回来。我觉得他们毫无关系，于是想试试是不是真的是这个问题，又来了一遍，果然遥控器又坏了。

千万不要卸载桌面~、系统用户界面、设置、以及你看不懂的那些东西啊！

有一些软件你不知道是干什么的，就别乱卸载。

![](https://pic4.zhimg.com/80/v2-54b62e6555615f6a6cfcacf2800cfb8f_1440w.webp)

## **七、设备安全**

**完事之后，记得关闭USB调试模式。**







