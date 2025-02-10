---
title: "Python实现Bilibili网站视频和音频下载器"
date: 2025-02-10T14:34:25+08:00
lastmod: 2025-02-10T15:00:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- Python
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

# Python实现Bilibili网站视频和音频下载器

注意：Bilibili网站数据中的视频（MP4）和音频（MP3）是分开的。

## 图形化用户界面最终效果

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost04/img20250210145433.png)

## 使用说明

1. **函数参数**：
   - `bv_id`: Bilibili视频的BV ID。
   - `cookie`: 发送请求所需的cookie。
   - `media_type`: 用于选择下载视频还是音频，默认为`video`。
   - `dir_path`: 指定保存文件的目录。

2. **功能实现**：
   - 函数首先发送请求并解析HTML，提取视频标题和媒体信息。
   - 根据`media_type`参数选择下载视频或音频。
   - 下载完成后，将文件保存到指定目录，并打印成功信息。


## 完整代码

使用前提：安装`requests`、`wxpython`，并从浏览器中获得自己的Cookie填入下面`download_bilibili_media`函数中。

```python
import os
import requests
import re
import json
import wx


class BilibiliDownloader(wx.Frame):
    def __init__(self):
        super().__init__(None, title="Bilibili 视频/音频下载器", size=(400, 400))

        # 初始化界面元素
        panel = wx.Panel(self)
        vbox = wx.BoxSizer(wx.VERTICAL)

        # BV ID 输入框
        self.bv_id_label = wx.StaticText(panel, label="视频 BV ID:")
        self.bv_id_input = wx.TextCtrl(panel)
        vbox.Add(self.bv_id_label, flag=wx.TOP | wx.LEFT, border=10)
        vbox.Add(self.bv_id_input, flag=wx.EXPAND | wx.LEFT | wx.RIGHT | wx.BOTTOM, border=10)

        # 音频/视频选择
        self.media_choice_label = wx.StaticText(panel, label="选择下载类型:")
        self.media_choice = wx.RadioBox(panel, label="下载类型", choices=["音频", "视频"], style=wx.RA_SPECIFY_ROWS)
        vbox.Add(self.media_choice_label, flag=wx.TOP | wx.LEFT, border=10)
        vbox.Add(self.media_choice, flag=wx.EXPAND | wx.LEFT | wx.RIGHT | wx.BOTTOM, border=10)

        # 目录选择
        self.dir_label = wx.StaticText(panel, label="保存目录:")
        self.dir_input = wx.TextCtrl(panel, style=wx.TE_READONLY)
        self.browse_button = wx.Button(panel, label="选择目录", size=(100, 30))
        vbox.Add(self.dir_label, flag=wx.TOP | wx.LEFT, border=10)
        vbox.Add(self.dir_input, flag=wx.EXPAND | wx.LEFT | wx.RIGHT | wx.BOTTOM, border=10)
        vbox.Add(self.browse_button, flag=wx.ALIGN_LEFT | wx.BOTTOM, border=10)

        # 下载按钮
        self.download_button = wx.Button(panel, label="下载", size=(100, 30))
        vbox.Add(self.download_button, flag=wx.ALL | wx.ALIGN_CENTER, border=10)

        # 进度条
        self.progress_bar = wx.Gauge(panel, range=100, style=wx.GA_HORIZONTAL)
        vbox.Add(self.progress_bar, flag=wx.EXPAND | wx.ALL, border=10)

        # 设置布局
        panel.SetSizer(vbox)

        # 绑定按钮事件
        self.browse_button.Bind(wx.EVT_BUTTON, self.on_browse)
        self.download_button.Bind(wx.EVT_BUTTON, self.on_download)

        # 记住上次选择的目录
        self.last_dir = wx.StandardPaths.Get().GetDocumentsDir()

        self.Show()

    def on_browse(self, event):
        dialog = wx.DirDialog(self, "选择目录", self.last_dir)
        if dialog.ShowModal() == wx.ID_OK:
            self.dir_input.SetValue(dialog.GetPath())
            self.last_dir = dialog.GetPath()
        dialog.Destroy()

    def on_download(self, event):
        bv_id = self.bv_id_input.GetValue().strip()
        media_type = 'audio' if self.media_choice.GetStringSelection() == "音频" else 'video'
        save_dir = self.dir_input.GetValue().strip()

        if not bv_id or not save_dir:
            wx.MessageBox("请确保 BV ID 和保存目录都已输入", "错误", wx.OK | wx.ICON_ERROR)
            return

            # 下载文件并更新进度
        self.download_bilibili_media(bv_id, save_dir, media_type)

    def download_bilibili_media(self, bv_id, dir_path, media_type):
        cookie = "buvid3=8F7865F6-456F-2DDC-0AD6-B7EA38BBC38890525infoc; b_nut=1733219390; _uuid=5533E2B1-293B-59B10-D4A6-76DC2619432420427infoc; buvid4=068192C5-543B-CE2A-E0C9-E3CDEBC3743E91165-024120309-Nficxoa62E6UeyU5C2SNm8mSEUsuV%2FLyrBvxTqOF18hHvJjkWcWuvr5wDBc4alZg; buvid_fp=20a5b8d5be257eeac5c1368d4adeea4b; header_theme_version=CLOSE; enable_web_push=DISABLE; home_feed_column=5; browser_resolution=1707-898; DedeUserID=213815864; DedeUserID__ckMd5=d5a3c935fd4c8e9c; rpdid=|(JJmYmYRmkm0J'u~JRkRR~mY; CURRENT_FNVAL=4048; CURRENT_QUALITY=64; bili_ticket=eyJhbGciOiJIUzI1NiIsImtpZCI6InMwMyIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MzkyMzQzMjIsImlhdCI6MTczODk3NTA2MiwicGx0IjotMX0.VKnyld09i1ydkfGPON7wmgNsD-SCFI5EFHdhLFGdT5o; bili_ticket_expires=1739234262; b_lsid=10F783E56_194E60AEAF4; SESSDATA=00e0165f%2C1754578283%2C7d1f4%2A22CjDZmgKExa3pb9b_pXlvUX-K194lqmeyP6NiiqRUSNzW6xS4yhTzim-nym20HLbKeW0SVmp0djFWM0Y2ME1CaHdKb1lSSVVBckVPU2dJMjVhSHFLMmdMSmU0VzRaamozRXo4eE9OUzJzRXBsb1BhVXVfWGZzaWZmeFZuQzN2cjRIWXlQRU5IVDh3IIEC; bili_jct=fd16d9466e68eb0184ef44114b11d36b; sid=gt93v2im"  # 请替换为你的cookie
        url = f'https://www.bilibili.com/video/{bv_id}'
        headers = {
            "Referer": url,
            "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36",
            "Cookie": cookie
        }

        # 发送请求
        response = requests.get(url=url, headers=headers)
        html = response.text

        # 解析数据: 提取视频标题
        title = re.findall('title="(.*?)"', html)[0]
        info = re.findall('window.__playinfo__=(.*?)</script>', html)[0]
        json_data = json.loads(info)

        # 获取媒体链接
        if media_type == 'video':
            media_url = json_data['data']['dash']['video'][0]['baseUrl']
            file_extension = '.mp4'
        elif media_type == 'audio':
            media_url = json_data['data']['dash']['audio'][0]['baseUrl']
            file_extension = '.mp3'

            # 文件保存路径
        file_path = os.path.join(dir_path, title + file_extension)

        # 创建进度对话框
        self.progress_bar.SetValue(0)

        try:
            media_content = requests.get(media_url, headers=headers, stream=True)
            total_length = int(media_content.headers.get('content-length', 0))
            with open(file_path, 'wb') as f:
                for data in media_content.iter_content(chunk_size=4096):
                    if data:
                        f.write(data)
                        self.update_progress_bar(f.tell(), total_length)
            wx.MessageBox(f"{media_type.capitalize()} '{title}' 下载成功！", "完成", wx.OK | wx.ICON_INFORMATION)
        except Exception as e:
            wx.MessageBox(f"下载失败: {str(e)}", "错误", wx.OK | wx.ICON_ERROR)

    def update_progress_bar(self, current, total):
        if total > 0:
            progress = min(100, int((current / total) * 100))
            self.progress_bar.SetValue(progress)


if __name__ == "__main__":
    app = wx.App(False)
    downloader = BilibiliDownloader()
    app.MainLoop()
```


## 参考资料

[Python下载b站视频](https://blog.csdn.net/Trb201013/article/details/136254473)







