---
title: "Windows系统PE盘制作教程"
date: 2024-11-23T18:34:25+08:00
lastmod: 2024-11-23T23:45:22+08:00
categories:
- 计算机
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


## 前言

由于电脑C盘烧了，我为了把数据导出来折腾了好久，最后成功使用PE盘把最关键的资料拷贝出来。这里记录一下相关的工具。


## WinPE系统

WinPE系统，是轻量级的Windows操作系统，可以安装到U盘里面。当电脑系统无法进入或崩溃时，可以作为紧急启动方式，对计算机进行系统重装或配置操作。

要求：

1. 准备一个8G以上的U盘
2. 备份U盘重要文件，制作过程中会格式化U盘。
3. 自行准备一个重装的ISO/GHO镜像文件拷贝到U盘里面（支持Windows7、8、10、11系统安装）

镜像文件可以到微软官网下载，也可以从系统之家这里网站下载。



# 常用工具

## 大白菜U盘启动盘制作工具完整使用教程

[大白菜官网](https://dbc.zjwtexm.cn/)

全网独家技术、完美兼容新旧主板

简单好用的U盘重装工具

支持GPT-UEFI启动 苹果电脑安装

大白菜是一款具有支持提取安装文件，并自动进行系统安装和引导修复过程等功能的装机软件。但很多用户做好U盘启动盘之后对如何安装感到迷茫，针对这个问题，大白菜在此向大家详细介绍下U盘启动BIOS重装系统的全教程，希望能够帮助到大家。

### 制作前的准备工作

1准备一个8G以上U盘

2参看下面教程开始制作u盘启动盘

3请在制作前备份U盘内重要数据，避免出现不必要的问题；

4个别杀软会将本软件的主程序或PE内工具软件报毒，还请理性判断；

5USB移动硬盘转接芯片的优劣品质，将会影响制作成功与否或可否正常启动。

### 第一步、开始制作U盘启动盘

1下载并安装好大白菜装机版，打开软件并插入U盘，选择“默认模式”，点击需要制作启动的设备，在模式选项中选择“USB-HDD”，格式选择“NTFS”

![](https://dbc.zjwtexm.cn/images/index/tutorial1.png)

2点击“一键制作成USB启动盘”

![](https://dbc.zjwtexm.cn/images/index/tutorial2.png)

3在弹出的信息提示窗口中，点击“是”(注：制作启动盘会格式化U盘，请提前备份好U盘数据!)

![](https://dbc.zjwtexm.cn/images/index/tutorial3.png)

4大白菜装机版U盘工具正对U盘写入大白菜相关数据，完成制作写入后（点击“是”进行模拟启动）

![](https://dbc.zjwtexm.cn/images/index/tutorial4.png)

5模拟电脑成功启动说明大白菜U盘启动盘制作成功，按住Ctrl+Alt可释放鼠标进行窗口关闭的操作

![](https://dbc.zjwtexm.cn/images/index/tutorial5.png)

U盘启动盘制作成功后，需要下载一个windows系统文件（就是win7系统、win10系统文件这类的）到U盘里，便可开始重装系统，这类系统文件一般可以去MSDN下载

6百度搜索msdn itellyou点击进入；

![](https://dbc.zjwtexm.cn/images/index/tutorial6.png)

7在这个页面，点击“操作系统”，里面有各种版本的操作系统，比如你要下载windows7，就点击它，在右侧找到你所需的系统版本，点击“详细信息”，复制ed2k链接，可以使用迅雷、旋风、百度网盘离线等工具下载；

![](https://dbc.zjwtexm.cn/images/index/tutorial7.png)

8下载完成后，找到下载好的WIN7 ISO/GHO镜像拷贝到U盘目录，由于ISO/GHO文件通常都比较大，可能需要等待5~10分钟

![](https://dbc.zjwtexm.cn/images/index/tutorial8.png)

将U盘设置为优先启动项

9查询该电脑机型的U盘启动快捷键，重启出现开机画面后按下此键，进入优先启动项设置界面，通过“↑↓”键选择U盘选项后回车进入大白菜winpe界面，如下图所示，选择带有USB字样的或者选择自己的U盘名称标识(这里我u盘名称就是Sandisk Cruzer pcp1.26)

![](https://dbc.zjwtexm.cn/images/index/tutorial9.png)

10进入大白菜主菜单后，通过“↑↓”键选择“【1】启动Win10 X64PE(2G以上内存)”后回车确认，成功进入winpe。

![](https://dbc.zjwtexm.cn/images/index/tutorial10.png)

### U盘重装系统

第一步：双击打开“大白菜一键装机”

![](https://dbc.zjwtexm.cn/images/index/tutorial11.png)

第二步：点击“打开”选存放镜像U盘位置（每个人存放不一样，能查询镜像的位置就行）

![](https://dbc.zjwtexm.cn/images/index/tutorial12.png)

第三步：进入到U盘位置，鼠标点击一下windows7系统，再移动到右下角点击“打开”

![](https://dbc.zjwtexm.cn/images/index/tutorial13.png)

第四步：在WIM文件镜像这个位置，选择windows7系统镜像，点击“确定”

![](https://dbc.zjwtexm.cn/images/index/tutorial14.png)

第五步：选择“Windows 7 系统，点击“系统盘（c盘）”再点击“执行”

![](https://dbc.zjwtexm.cn/images/index/tutorial15.png)

第六步：勾选windows7系统的网卡和usb驱动安装（默认安装也可以），再点击“是”

![](https://dbc.zjwtexm.cn/images/index/tutorial16.png)

第七步：Win7系统进行安装时，勾选“完成后重启”重启电脑并拔掉U盘（以免重启时再次进入大白菜PE界面）

![](https://dbc.zjwtexm.cn/images/index/tutorial17.png)

第八步：正在部署系统，等待3~5分钟

![](https://dbc.zjwtexm.cn/images/index/tutorial18.png)

第九步：成功安装系统

![](https://dbc.zjwtexm.cn/images/index/tutorial19.png)

系统安装完成后重启电脑，会进行系统的部署并安装驱动程序，耐心等待部署完成，即可进入安装好的系统

### 大白菜装机小提示：

如果您在重装前准备好了系统镜像，并将其保存在U盘启动盘或重装电脑除系统盘（一般指C盘）以外的分区中，可在第一步中选择“安装系统”，选择准备好的系统镜像和安装路径，一般选择C盘，完成后点击“执行”。接下来的操作如上所述，在此就不再重复了

以上就是大白菜U盘启动重装系统完整教程步骤，如果还不知道怎么重装的朋友们可以参考上述教程，希望能够对大家有所帮助!

## 微PE工具箱

[官网](https://www.wepe.com.cn)

根据官网教程做即可。












