---
title: "Python实现P站视频下载器"
date: 2025-02-10T16:34:25+08:00
lastmod: 2025-02-10T16:53:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- Python
- 豫游之乐
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

# Python实现P站视频下载器

## Phub

[文档链接](https://phub.readthedocs.io/en/latest/)

PHUB is an easy-to-use API wrapper for Pornhub. It can access most used or useful PH features, such as video searching, account features, video downloading, and more.

## 本地运行

开启VPN，填入URL，启动程序即可

```python
import phub

# Initialise a client
client = phub.Client()

url = "input the url of the video"

# Fetch and download a video
video = client.get(url)
video.download('./'+ str(id) + '.mp4')
```

## GUI界面设计及代码实现

让我们设计一个使用 `wxPython` 实现的完整、结构美观的GUI界面来下载视频，特别是来自 Pornhub 的视频。以下代码实现了您要求的特性，包括输入URL、下载按钮、目录选择、下载进度条等。

下面的代码展示了一个完整的 Python 程序，创建了一个用于下载 Pornhub 视频的 GUI。

```python
import wx
import os
import threading
import phub

class VideoDownloaderApp(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(VideoDownloaderApp, self).__init__(*args, **kwargs)

        self.SetTitle("Pornhub 视频下载器")
        self.SetSize((400, 250))
        self.SetBackgroundColour(wx.Colour(240, 240, 240))

        self.url_label = wx.StaticText(self, label="视频 URL:")
        self.url_text = wx.TextCtrl(self)

        self.dir_label = wx.StaticText(self, label="下载目录:")
        self.dir_text = wx.TextCtrl(self, style=wx.TE_READONLY)

        self.select_dir_button = wx.Button(self, label="选择下载目录")
        self.download_button = wx.Button(self, label="开始下载")
        
        self.progress = wx.Gauge(self, range=100)

        self.sizer = wx.BoxSizer(wx.VERTICAL)
        self._setup_layout()
        
        self.Bind(wx.EVT_BUTTON, self.on_select_directory, self.select_dir_button)
        self.Bind(wx.EVT_BUTTON, self.on_download, self.download_button)

        # 记住上次选择的目录
        self.last_dir = os.path.expanduser("~")

        # For simplicity, you can adjust as needed
        self.SetSizer(self.sizer)

    def _setup_layout(self):
        self.sizer.Add(self.url_label, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.url_text, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.dir_label, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.dir_text, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.select_dir_button, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.download_button, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.progress, 0, wx.ALL | wx.EXPAND, 5)

    def on_select_directory(self, event):
        with wx.DirDialog(self, "选择下载目录", self.last_dir, style=wx.DD_DEFAULT_STYLE) as dlg:
            if dlg.ShowModal() == wx.ID_OK:
                self.last_dir = dlg.GetPath()
                self.dir_text.SetValue(self.last_dir)

    def on_download(self, event):
        url = self.url_text.GetValue().strip()
        if not url:
            wx.MessageBox("请输入有效的URL", "错误", wx.OK | wx.ICON_ERROR)
            return

        threading.Thread(target=self.start_download, args=(url,)).start()

    def start_download(self, url):
        self.progress.SetValue(0)
        id = url.split("viewkey=")[-1]  # 提取ID
        downloader = phub.Client()

        try:
            video = downloader.get(url)
            video.download(os.path.join(self.last_dir, f"{id}.mp4"))
            for i in range(1, 101):
                self.progress.SetValue(i)  # 在实际下载中，应更新进度条此处仅为示例
                wx.MilliSleep(50)  # 模拟下载进度
            wx.CallAfter(self.show_message, "下载完成！")
        except Exception as e:
            wx.CallAfter(self.show_message, "下载失败: " + str(e))

    def show_message(self, message):
        wx.MessageBox(message, "提示", wx.OK | wx.ICON_INFORMATION)


if __name__ == "__main__":
    app = wx.App(False)
    frame = VideoDownloaderApp(None)
    frame.Show()
    app.MainLoop()
```

### 主要组件说明

1. **窗口设置**：
   - 使用 `wx.Frame` 创建主窗口并设置标题和窗口大小。
   - 使用 `wx.BoxSizer` 进行布局，使所有控件能美观地排列。

2. **控件**：
   - `StaticText` 用于标签。
   - `TextCtrl` 用于输入URL和显示选择的下载目录。
   - `Button` 用于选择目录和下载视频。
   - `Gauge` 用作下载进度条。

3. **目录选择**：
   - 使用 `wx.DirDialog` 让用户选择下载目录，并记住上次选择的路径。

4. **下载逻辑**：
   - 在新的线程中执行下载，以避免界面冻结。 
   - 获取视频 ID 并下载，进度条模拟了下载过程中的进度更新。

5. **错误处理**：
   - 添加错误处理，确保如果输入的URL无效或者下载失败，用户会收到相应提示。

### 注意事项

- 确保您已经在运行该代码的 Python 环境中安装了 `wxPython` 和 `phub` 库。
- 由于网络请求和文件操作在实际下载过程中可能会引发异常，建议在真实场景中添加详细的异常处理逻辑。
- 下载进度的实现只是一个模拟。在实际应用中，您需要在下载过程中取得真实的进度更新。







