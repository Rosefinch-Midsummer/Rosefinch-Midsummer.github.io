---
title: "Python实现文章下载器"
date: 2025-02-10T15:01:25+08:00
lastmod: 2025-02-10T15:54:22+08:00
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

# Python实现文章下载器

## 说明

支持平台：知乎（回答、文章、专栏和视频）、CSDN、微信公众号

区别：是否下载图片到本地（有无Local）

## 图形化用户界面

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost04/img20250210152241.png)


## 完整代码

说明：下载知乎文章需要使用自己的Cookie

前提：安装`wxpython`、`markdownify`、`requests`、`BeautifulSoup4`、`tqdm`

把下面五个Python文件放到同一个目录下，执行`GUI.py`即可开启图形化用户界面。

### GUI.py

```python
import wx
import os
import threading
from csdn_downloader_img import CsdnParserLocal, CsdnParser
from zhihu_downloader_img import ZhihuParserLocal, ZhihuParser
from weixin_downloader_img import WeixinParserLocal, WeixinParser


class DownloaderApp(wx.Frame):
    def __init__(self, *args, **kwargs):
        super(DownloaderApp, self).__init__(*args, **kwargs)

        self.SetTitle("文章下载器")
        self.SetSize((420, 380))

        self.url_label = wx.StaticText(self, label="网址:")
        self.url_text = wx.TextCtrl(self)

        self.cookie_label = wx.StaticText(self, label="Cookie (若适用):")
        self.cookie_text = wx.TextCtrl(self, style=wx.TE_MULTILINE)

        self.type_label = wx.StaticText(self, label="选择内容类型:")
        self.type_choice = wx.Choice(self,
                                     choices=["CSDN文章", "知乎回答", "知乎文章", "微信文章", "知乎视频", "知乎专栏"])
        self.type_choice.SetSelection(0)  # 默认选择第一个

        self.local_checkbox = wx.CheckBox(self, label="下载图片到本地")
        self.local_checkbox.SetValue(True)

        self.select_dir_button = wx.Button(self, label="选择下载目录")
        self.dir_text = wx.TextCtrl(self, style=wx.TE_READONLY)

        self.download_button = wx.Button(self, label="开始下载")
        self.progress = wx.Gauge(self, range=100)

        self.sizer = wx.BoxSizer(wx.VERTICAL)
        self._setup_layout()

        self.Bind(wx.EVT_BUTTON, self.on_select_directory, self.select_dir_button)
        self.Bind(wx.EVT_BUTTON, self.on_download, self.download_button)

        self.last_dir = None

    def _setup_layout(self):
        self.sizer.Add(self.url_label, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.url_text, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.cookie_label, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.cookie_text, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.type_label, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.type_choice, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.local_checkbox, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.select_dir_button, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.dir_text, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.download_button, 0, wx.ALL | wx.EXPAND, 5)
        self.sizer.Add(self.progress, 0, wx.ALL | wx.EXPAND, 5)

        self.SetSizer(self.sizer)

    def on_select_directory(self, event):
        with wx.DirDialog(self, "选择下载目录", style=wx.DD_DEFAULT_STYLE) as dlg:
            if dlg.ShowModal() == wx.ID_OK:
                self.last_dir = dlg.GetPath()
                self.dir_text.SetValue(self.last_dir)

    def on_download(self, event):
        url = self.url_text.GetValue()
        cookies = self.cookie_text.GetValue() if self.cookie_text.IsEnabled() else None
        download_locally = self.local_checkbox.GetValue()
        content_type = self.type_choice.GetStringSelection()

        download_thread = threading.Thread(target=self.start_download,
                                           args=(url, cookies, download_locally, content_type))
        download_thread.start()

    def start_download(self, url, cookies, download_locally, content_type):
        if download_locally and self.last_dir:
            os.chdir(self.last_dir)  # 设置下载目录

        self.progress.SetValue(0)

        try:
            # 根据URL判断类型，调用相应的解析器进行下载
            if "csdn" in url and "CSDN" in content_type:
                parser = CsdnParserLocal() if download_locally else CsdnParser()
                # 这里调用下载方法并假设返回处理好的内容
                parser.judge_type(url)

            elif "zhihu" in url:
                parser = ZhihuParserLocal(cookies) if download_locally else ZhihuParser(cookies)
                parser.judge_type(url)

            elif "mp.weixin" in url and "微信" in content_type:
                parser = WeixinParserLocal() if download_locally else WeixinParser()
                parser.judge_type(url)

            wx.CallAfter(self.show_message, "下载完成")
        except Exception as e:
            wx.CallAfter(self.show_message, "下载失败: " + str(e))

    def show_message(self, message):
        wx.MessageBox(message, "提示", wx.OK | wx.ICON_INFORMATION)


if __name__ == "__main__":
    app = wx.App(False)
    frame = DownloaderApp(None)
    frame.Show()
    app.MainLoop()
```

### util.py

```python
import re


def insert_new_line(soup, element, num_breaks):
    """
    在指定位置插入换行符
    """
    for _ in range(num_breaks):
        new_line = soup.new_tag('br')
        element.insert_after(new_line)


def get_article_date(soup, name):
    """
    从页面中提取文章日期
    """
    date_element = soup.select_one(name)
    if date_element:
        match = re.search(r"\d{4}-\d{2}-\d{2}", date_element.get_text())
        if match:
            return match.group().replace('-', '')
    return "Unknown"


def get_article_date_weixin(date_element):
    """
    从页面中提取文章日期
    """
    for script in date_element:
        # 获取 JavaScript 代码
        js_code = script.string
        if js_code:
            # 尝试提取 createTime
            match = re.search(r"\d{4}-\d{2}-\d{2}", js_code)
            if match:
                return match.group().replace('-', '')
    return "Unknown"


def download_image(url, save_path, session):
    """
    从指定url下载图片并保存到本地
    """
    if url.startswith("data:image/"):
        # 如果链接以 "data:" 开头，则直接写入数据到文件
        with open(save_path, "wb") as f:
            f.write(url.split(",", 1)[1].encode("utf-8"))
    else:
        response = session.get(url)
        with open(save_path, "wb") as f:
            f.write(response.content)


def download_video(url, save_path, session):
    """
    从指定url下载视频并保存到本地
    """
    response = session.get(url)
    with open(save_path, "wb") as f:
        f.write(response.content)


def get_valid_filename(s):
    """
    将字符串转换为有效的文件名
    """
    # 检查第一个字符是否为特殊符号或数字
    if s and (not s[0].isalpha() or s[0].isdigit()):
        s = s[1:]
    s = str(s).strip().replace(' ', '_')
    return re.sub(r'(?u)[^-\w_]', '', s)

def process_markdown_content(content):
    # 处理标题，前面添加空格
    content = re.sub(r'^(#+)', r' \1', content, flags=re.MULTILINE)

    # 去掉 \_ 中的 \
    content = re.sub(r'\\_', '_', content)

    # 去除 \$ 前后的空格和反斜杠 \
    content = re.sub(r'\\?\s*\$\s*', '$', content)

    # 在公式的 $ 左右添加空格
    # content = re.sub(r'(\$)([^$]+)(\$)', r' \1\2\3 ', content)

    return content
```


### zhihu-downloader_img.py

```python
import os
import urllib.parse

import requests
from bs4 import BeautifulSoup
from markdownify import markdownify as md
from urllib.parse import unquote, urlparse, parse_qs
from tqdm import tqdm
import json
from util import insert_new_line, get_article_date, process_markdown_content, download_image, download_video, get_valid_filename


class ZhihuParserLocal:
    def __init__(self, cookies, hexo_uploader=False):
        self.hexo_uploader = hexo_uploader  # 是否为 hexo 博客上传
        self.cookies = cookies  # 登录知乎后的 cookies
        self.session = requests.Session()  # 创建会话
        self.user_agents = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"  # 用户代理
        self.headers = {  # 请求头
            'User-Agent': self.user_agents,
            'Accept-Language': 'en,zh-CN;q=0.9,zh;q=0.8',
            'Cookie': self.cookies
        }
        self.session.headers.update(self.headers)  # 更新会话的请求头
        self.soup = None  # 存储页面的 BeautifulSoup 对象

    def check_connect_error(self, target_link):
        """
        检查是否连接错误
        """
        try:
            response = self.session.get(target_link)
            response.raise_for_status()
        except requests.exceptions.HTTPError as err:
            print(f"HTTP error occurred: {err}")

        except requests.exceptions.RequestException as err:
            print(f"Error occurred: {err}")

        self.soup = BeautifulSoup(response.content, "html.parser")
        if self.soup.text.find("有问题，就会有答案打开知乎App在「我的页」右上角打开扫一扫其他扫码方式") != -1:
            print("Cookies are required to access the article.")

        if self.soup.text.find("你似乎来到了没有知识存在的荒原") != -1:
            print("The page does not exist.")

    def judge_type(self, target_link):
        """
        判断url类型
        """
        if target_link.find("column") != -1:
            # 如果是专栏
            title = self.parse_zhihu_column(target_link)

        elif target_link.find("answer") != -1:
            # 如果是回答
            title = self.parse_zhihu_answer(target_link)

        elif target_link.find("zvideo") != -1:
            # 如果是视频
            title = self.parse_zhihu_zvideo(target_link)

        else:
            # 如果是单篇文章
            title = self.parse_zhihu_article(target_link)

        return title

    def save_and_transform(self, title_element, content_element, author, target_link, date=None):
        """
        转化并保存为 Markdown 格式文件
        """
        # 获取标题和内容
        if title_element is not None:
            title = title_element.text.strip()
        else:
            title = "Untitled"

        # 防止文件名称太长，加载不出图像
        # markdown_title = get_valid_filename(title[-20:-1])
        # 如果觉得文件名太怪不好管理，那就使用全名
        markdown_title = get_valid_filename(title)

        if date:
            markdown_title = f"({date}){markdown_title}_{author}"
        else:
            markdown_title = f"{markdown_title}_{author}"

        if content_element is not None:
            # 将 css 样式移除
            for style_tag in content_element.find_all("style"):
                style_tag.decompose()

            for img_lazy in content_element.find_all("img", class_=lambda x: 'lazy' in x if x else True):
                img_lazy.decompose()

            # 处理内容中的标题
            for header in content_element.find_all(['h1', 'h2', 'h3', 'h4', 'h5', 'h6']):
                header_level = int(header.name[1])  # 从标签名中获取标题级别（例如，'h2' -> 2）
                header_text = header.get_text(strip=True)  # 提取标题文本
                # 转换为 Markdown 格式的标题
                markdown_header = f"{'#' * header_level} {header_text}"
                insert_new_line(self.soup, header, 1)
                header.replace_with(markdown_header)

            # 处理回答中的图片
            for img in content_element.find_all("img"):
                if 'src' in img.attrs:
                    img_url = img.attrs['src']
                else:
                    continue

                img_name = urllib.parse.quote(os.path.basename(img_url))
                img_path = f"{markdown_title}/{img_name}"

                extensions = ['.jpg', '.png', '.gif']  # 可以在此列表中添加更多的图片格式

                # 如果图片链接中图片后缀后面还有字符串则直接截停
                for ext in extensions:
                    index = img_path.find(ext)
                    if index != -1:
                        img_path = img_path[:index + len(ext)]
                        break  # 找到第一个匹配的格式后就跳出循环

                img["src"] = img_path

                # 下载图片并保存到本地
                os.makedirs(os.path.dirname(img_path), exist_ok=True)
                download_image(img_url, img_path, self.session)

                # 在图片后插入换行符
                insert_new_line(self.soup, img, 1)

            # 在图例后面加上换行符
            for figcaption in content_element.find_all("figcaption"):
                insert_new_line(self.soup, figcaption, 2)

            # 处理链接
            for link in content_element.find_all("a"):
                if 'href' in link.attrs:
                    original_url = link.attrs['href']

                    # 解析并解码 URL
                    parsed_url = urlparse(original_url)
                    query_params = parse_qs(parsed_url.query)
                    target_url = query_params.get('target', [original_url])[
                        0]  # 使用原 URL 作为默认值
                    article_url = unquote(target_url)  # 解码 URL

                    # 如果没有 data-text 属性，则使用文章链接作为标题
                    if 'data-text' not in link.attrs:
                        article_title = article_url
                    else:
                        article_title = link.attrs['data-text']

                    markdown_link = f"[{article_title}]({article_url})"

                    link.replace_with(markdown_link)

            # 提取并存储数学公式
            math_formulas = []
            math_tags = []
            for math_span in content_element.select("span.ztext-math"):
                latex_formula = math_span['data-tex']
                # math_formulas.append(latex_formula)
                # math_span.replace_with("@@MATH@@")
                # 使用特殊标记标记位置
                if latex_formula.find("\\tag") != -1:
                    math_tags.append(latex_formula)
                    insert_new_line(self.soup, math_span, 1)
                    math_span.replace_with("@@MATH_FORMULA@@")
                else:
                    math_formulas.append(latex_formula)
                    math_span.replace_with("@@MATH@@")

            # 获取文本内容
            content = content_element.decode_contents().strip()
            # 转换为 markdown
            content = md(content)

            # 将特殊标记替换为 LaTeX 数学公式
            for formula in math_formulas:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH@@", "$" + "{% raw %}" + formula + "{% endraw %}" + "$", 1)
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find('$') != -1:
                        content = content.replace("@@MATH@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH@@", f"${formula}$", 1)

            for formula in math_tags:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH\_FORMULA@@",
                        "$$" + "{% raw %}" + formula + "{% endraw %}" + "$$",
                        1,
                    )
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find("$") != -1:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"$${formula}$$", 1)

        else:
            content = ""

        # 转化为 Markdown 格式
        if content:
            markdown = f"# {title}\n\n **Author:** [{author}]\n\n **Link:** [{target_link}]\n\n{content}"
        else:
            markdown = f"# {title}\n\n Content is empty."

        # 保存 Markdown 文件
        with open(f"{markdown_title}.md", "w", encoding="utf-8") as f:
            f.write(markdown)

        return markdown_title

    def parse_zhihu_zvideo(self, target_link):
        """
        解析知乎视频并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)
        data = json.loads(self.soup.select_one(
            "div.ZVideo-video")['data-zop'])  # 获取视频数据

        # match = re.search(r"\d{4}-\d{2}-\d{2}",
        #                   soup.select_one("div.ZVideo-meta").text) # 获取日期

        # if match:
        #     # 将日期中的"-"替换为空字符以格式化为YYYYMMDD
        #     date = match.group().replace('-', '')
        # else:
        #     date = "Unknown"

        date = get_article_date(self.soup, "div.ZVideo-meta")

        markdown_title = f"({date}){data['authorName']}_{data['title']}/{data['authorName']}_{data['title']}.mp4"

        video_url = None
        script = self.soup.find('script', id='js-initialData')
        if script:
            data = json.loads(script.text)
            try:
                videos = data['initialState']['entities']['zvideos']
                for video_id, video_info in videos.items():
                    if 'playlist' in video_info['video']:
                        for quality, details in video_info['video']['playlist'].items():
                            video_url = details['playUrl']
            except KeyError as e:
                print("Key error in parsing JSON data:", e)
                return None
        else:
            print("No suitable script tag found for video data")
            return None

        os.makedirs(os.path.dirname(markdown_title), exist_ok=True)

        download_video(video_url, markdown_title, self.session)

        return markdown_title

    def parse_zhihu_article(self, target_link):
        """
        解析知乎文章并保存为Markdown格式文件
        """
        self.check_connect_error(target_link)
        title_element = self.soup.select_one("h1.Post-Title")
        content_element = self.soup.select_one("div.Post-RichTextContainer")
        date = get_article_date(self.soup, "div.ContentItem-time")
        author = self.soup.select_one('div.AuthorInfo').find(
            'meta', {'itemprop': 'name'}).get('content')

        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def parse_zhihu_answer(self, target_link):
        """
        解析知乎回答并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)
        # 找到回答标题、内容、作者所在的元素
        title_element = self.soup.select_one("h1.QuestionHeader-title")
        content_element = self.soup.select_one("div.RichContent-inner")
        date = get_article_date(self.soup, "div.ContentItem-time")
        author = self.soup.select_one('div.AuthorInfo').find(
            'meta', {'itemprop': 'name'}).get('content')

        # 解析知乎文章并保存为Markdown格式文件
        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def load_processed_articles(self, filename):
        """
        从文件加载已处理文章的ID。
        """
        if not os.path.exists(filename):
            return set()
        with open(filename, 'r', encoding='utf-8') as file:
            return set(file.read().splitlines())

    def save_processed_article(self, filename, article_id):
        """
        将处理过的文章ID保存到文件。
        """
        with open(filename, 'a', encoding='utf-8') as file:
            file.write(article_id + '\n')

    def parse_zhihu_column(self, target_link):
        """
        解析知乎专栏并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)

        # 将所有文章放在一个以专栏标题命名的文件夹中
        title = self.soup.text.split('-')[0].strip()
        total_articles = int(self.soup.text.split(
            '篇内容')[0].split('·')[-1].strip())  # 总文章数
        folder_name = get_valid_filename(title)
        os.makedirs(folder_name, exist_ok=True)
        os.chdir(folder_name)

        processed_filename = "zhihu_processed_articles.txt"
        processed_articles = self.load_processed_articles(processed_filename)

        # 获取所有文章链接
        offset = 0
        total_parsed = 0

        # # 首先获取总文章数
        # api_url = f"/api/v4/columns/{target_link.split('/')[-1]}/items?limit=1&offset=0"
        # response = session.get(f"https://www.zhihu.com{api_url}")
        # total_articles = response.json()["paging"]["totals"]

        # 计算已处理的文章数
        already_processed = len(processed_articles)

        # 初始化进度条，从已处理的文章数开始
        progress_bar = tqdm(total=total_articles,
                            initial=already_processed, desc="解析文章")

        while True:
            api_url = f"/api/v4/columns/{target_link.split('/')[-1]}/items?limit=10&offset={offset}"
            response = self.session.get(f"https://www.zhihu.com{api_url}")
            data = response.json()

            for item in data["data"]:
                if item["type"] == "zvideo":
                    video_id = str(item["id"])
                    if video_id in processed_articles:
                        continue

                    video_link = f"https://www.zhihu.com/zvideo/{video_id}"
                    self.parse_zhihu_zvideo(video_link)
                    self.save_processed_article(processed_filename, video_id)
                    progress_bar.update(1)  # 更新进度条

                elif item["type"] == "article":
                    article_id = str(item["id"])
                    if article_id in processed_articles:
                        continue

                    article_link = f"https://zhuanlan.zhihu.com/p/{article_id}"
                    self.parse_zhihu_article(article_link)
                    self.save_processed_article(processed_filename, article_id)
                    progress_bar.update(1)  # 更新进度条

                elif item["type"] == "answer":
                    answer_id = str(item["id"])
                    if answer_id in processed_articles:
                        continue

                    answer_link = f"https://www.zhihu.com/question/{item['question']['id']}/answer/{answer_id}"
                    self.judge_type(answer_link)
                    self.save_processed_article(processed_filename, answer_id)
                    progress_bar.update(1)

            if data["paging"]["is_end"]:
                break

            offset += 10

        progress_bar.close()  # 完成后关闭进度条
        os.remove(processed_filename)  # 删除已处理文章的ID文件
        return folder_name

class ZhihuParser:
    def __init__(self, cookies, hexo_uploader=False):
        self.hexo_uploader = hexo_uploader  # 是否为 hexo 博客上传
        self.cookies = cookies  # 登录知乎后的 cookies
        self.session = requests.Session()  # 创建会话
        self.user_agents = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"  # 用户代理
        self.headers = {  # 请求头
            'User-Agent': self.user_agents,
            'Accept-Language': 'en,zh-CN;q=0.9,zh;q=0.8',
            'Cookie': self.cookies
        }
        self.session.headers.update(self.headers)  # 更新会话的请求头
        self.soup = None  # 存储页面的 BeautifulSoup 对象

    def check_connect_error(self, target_link):
        """
        检查是否连接错误
        """
        try:
            response = self.session.get(target_link)
            response.raise_for_status()
        except requests.exceptions.HTTPError as err:
            print(f"HTTP error occurred: {err}")

        except requests.exceptions.RequestException as err:
            print(f"Error occurred: {err}")

        self.soup = BeautifulSoup(response.content, "html.parser")
        if self.soup.text.find("有问题，就会有答案打开知乎App在「我的页」右上角打开扫一扫其他扫码方式") != -1:
            print("Cookies are required to access the article.")

        if self.soup.text.find("你似乎来到了没有知识存在的荒原") != -1:
            print("The page does not exist.")

    def judge_type(self, target_link):
        """
        判断url类型
        """
        if target_link.find("column") != -1:
            # 如果是专栏
            title = self.parse_zhihu_column(target_link)

        elif target_link.find("answer") != -1:
            # 如果是回答
            title = self.parse_zhihu_answer(target_link)

        elif target_link.find("zvideo") != -1:
            # 如果是视频
            title = self.parse_zhihu_zvideo(target_link)

        else:
            # 如果是单篇文章
            title = self.parse_zhihu_article(target_link)

        return title

    def save_and_transform(self, title_element, content_element, author, target_link, date=None):
        """
        转化并保存为 Markdown 格式文件
        """
        # 获取标题和内容
        title = title_element.text.strip() if title_element is not None else "Untitled"
        markdown_title = get_valid_filename(title) if date is None else f"({date}){get_valid_filename(title)}_{author}"

        if content_element is not None:
            # 将 css 样式移除
            for style_tag in content_element.find_all("style"):
                style_tag.decompose()

            for img_lazy in content_element.find_all("img", class_=lambda x: 'lazy' in x if x else True):
                img_lazy.decompose()

            # 处理内容中的标题
            for header in content_element.find_all(['h1', 'h2', 'h3', 'h4', 'h5', 'h6']):
                header_level = int(header.name[1])
                header_text = header.get_text(strip=True)
                markdown_header = f"{'#' * header_level} {header_text}"
                insert_new_line(self.soup, header, 1)
                header.replace_with(markdown_header)

            # 处理回答中的图片
            for figure in content_element.find_all("figure"):
                img = figure.find("img")
                if img and 'src' in img.attrs:
                    img_url = img.attrs['src']

                    # 提取 figcaption 内容
                    figcaption = figure.find("figcaption")
                    figcaption_text = figcaption.get_text(strip=True) if figcaption else "Image"

                    # 替换 img 标签为 Markdown 图片格式, 使用 figcaption 内容作为描述
                    markdown_img = f"![{figcaption_text}]({img_url})"

                    # 在 img 后插入 Markdown 格式字符串
                    img.insert_after(markdown_img)
                    img.extract()  # 移除 img 标签

                    # 若存在 figcaption，移除它
                    if figcaption:
                        figcaption.extract()

                    # 在插入的 Markdown 图片后插入换行符
                    next_sibling = img.find_next_sibling()
                    if next_sibling is not None:
                        insert_new_line(self.soup, next_sibling, 1)
                    else:
                        # 如果没有下一个兄弟元素，可以选择在内容末尾插入换行符
                        insert_new_line(self.soup, content_element, 1)  # 或者一个合适的元素

                # 处理链接
            for link in content_element.find_all("a"):
                if 'href' in link.attrs:
                    original_url = link.attrs['href']
                    parsed_url = urlparse(original_url)
                    query_params = parse_qs(parsed_url.query)
                    target_url = query_params.get('target', [original_url])[0]
                    article_url = unquote(target_url)

                    article_title = link.attrs['data-text'] if 'data-text' in link.attrs else article_url
                    markdown_link = f"[{article_title}]({article_url})"

                    link.replace_with(markdown_link)

            # 提取并存储数学公式
            math_formulas = []
            math_tags = []
            for math_span in content_element.select("span.ztext-math"):
                latex_formula = math_span['data-tex']
                if latex_formula.find("\\tag") != -1:
                    math_tags.append(latex_formula)
                    insert_new_line(self.soup, math_span, 1)
                    math_span.replace_with("@@MATH_FORMULA@@")
                else:
                    math_formulas.append(latex_formula)
                    math_span.replace_with("@@MATH@@")

                    # 获取文本内容
            content = content_element.decode_contents().strip()
            content = md(content)

            # 替换数学公式
            for formula in math_formulas:
                if self.hexo_uploader:
                    content = content.replace("@@MATH@@", "$" + "{% raw %}" + formula + "{% endraw %}" + "$", 1)
                else:
                    if formula.find('$') != -1:
                        content = content.replace("@@MATH@@", f"{formula}", 1)
                    else:
                        content = content.replace("@@MATH@@", f"${formula}$", 1)

            for formula in math_tags:
                if self.hexo_uploader:
                    content = content.replace("@@MATH_FORMULA@@", "$$" + "{% raw %}" + formula + "{% endraw %}" + "$$",
                                              1)
                else:
                    if formula.find("$") != -1:
                        content = content.replace("@@MATH_FORMULA@@", f"{formula}", 1)
                    else:
                        content = content.replace("@@MATH_FORMULA@@", f"$${formula}$$", 1)

        else:
            content = ""

        if content:
            markdown = f"# {title}\n\n **Author:** [{author}]\n\n **Link:** [{target_link}]\n\n{content}"
        else:
            markdown = f"# {title}\n\n Content is empty."

        # 保存 Markdown 文件

        # 在保存 Markdown 前处理内容
        markdown = process_markdown_content(markdown)

        with open(f"{markdown_title}.md", "w", encoding="utf-8") as f:
            f.write(markdown)

    def parse_zhihu_zvideo(self, target_link):
        """
        解析知乎视频并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)
        data = json.loads(self.soup.select_one(
            "div.ZVideo-video")['data-zop'])  # 获取视频数据

        # match = re.search(r"\d{4}-\d{2}-\d{2}",
        #                   soup.select_one("div.ZVideo-meta").text) # 获取日期

        # if match:
        #     # 将日期中的"-"替换为空字符以格式化为YYYYMMDD
        #     date = match.group().replace('-', '')
        # else:
        #     date = "Unknown"

        date = get_article_date(self.soup, "div.ZVideo-meta")

        markdown_title = f"({date}){data['authorName']}_{data['title']}/{data['authorName']}_{data['title']}.mp4"

        video_url = None
        script = self.soup.find('script', id='js-initialData')
        if script:
            data = json.loads(script.text)
            try:
                videos = data['initialState']['entities']['zvideos']
                for video_id, video_info in videos.items():
                    if 'playlist' in video_info['video']:
                        for quality, details in video_info['video']['playlist'].items():
                            video_url = details['playUrl']
            except KeyError as e:
                print("Key error in parsing JSON data:", e)
                return None
        else:
            print("No suitable script tag found for video data")
            return None

        os.makedirs(os.path.dirname(markdown_title), exist_ok=True)

        download_video(video_url, markdown_title, self.session)

        return markdown_title

    def parse_zhihu_article(self, target_link):
        """
        解析知乎文章并保存为Markdown格式文件
        """
        self.check_connect_error(target_link)
        title_element = self.soup.select_one("h1.Post-Title")
        content_element = self.soup.select_one("div.Post-RichTextContainer")
        date = get_article_date(self.soup, "div.ContentItem-time")
        author = self.soup.select_one('div.AuthorInfo').find(
            'meta', {'itemprop': 'name'}).get('content')

        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def parse_zhihu_answer(self, target_link):
        """
        解析知乎回答并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)
        # 找到回答标题、内容、作者所在的元素
        title_element = self.soup.select_one("h1.QuestionHeader-title")
        content_element = self.soup.select_one("div.RichContent-inner")
        date = get_article_date(self.soup, "div.ContentItem-time")
        author = self.soup.select_one('div.AuthorInfo').find(
            'meta', {'itemprop': 'name'}).get('content')

        # 解析知乎文章并保存为Markdown格式文件
        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def load_processed_articles(self, filename):
        """
        从文件加载已处理文章的ID。
        """
        if not os.path.exists(filename):
            return set()
        with open(filename, 'r', encoding='utf-8') as file:
            return set(file.read().splitlines())

    def save_processed_article(self, filename, article_id):
        """
        将处理过的文章ID保存到文件。
        """
        with open(filename, 'a', encoding='utf-8') as file:
            file.write(article_id + '\n')

    def parse_zhihu_column(self, target_link):
        """
        解析知乎专栏并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)

        # 将所有文章放在一个以专栏标题命名的文件夹中
        title = self.soup.text.split('-')[0].strip()
        total_articles = int(self.soup.text.split(
            '篇内容')[0].split('·')[-1].strip())  # 总文章数
        folder_name = get_valid_filename(title)
        os.makedirs(folder_name, exist_ok=True)
        os.chdir(folder_name)

        processed_filename = "zhihu_processed_articles.txt"
        processed_articles = self.load_processed_articles(processed_filename)

        # 获取所有文章链接
        offset = 0
        total_parsed = 0

        # # 首先获取总文章数
        # api_url = f"/api/v4/columns/{target_link.split('/')[-1]}/items?limit=1&offset=0"
        # response = session.get(f"https://www.zhihu.com{api_url}")
        # total_articles = response.json()["paging"]["totals"]

        # 计算已处理的文章数
        already_processed = len(processed_articles)

        # 初始化进度条，从已处理的文章数开始
        progress_bar = tqdm(total=total_articles,
                            initial=already_processed, desc="解析文章")

        while True:
            api_url = f"/api/v4/columns/{target_link.split('/')[-1]}/items?limit=10&offset={offset}"
            response = self.session.get(f"https://www.zhihu.com{api_url}")
            data = response.json()

            for item in data["data"]:
                if item["type"] == "zvideo":
                    video_id = str(item["id"])
                    if video_id in processed_articles:
                        continue

                    video_link = f"https://www.zhihu.com/zvideo/{video_id}"
                    self.parse_zhihu_zvideo(video_link)
                    self.save_processed_article(processed_filename, video_id)
                    progress_bar.update(1)  # 更新进度条

                elif item["type"] == "article":
                    article_id = str(item["id"])
                    if article_id in processed_articles:
                        continue

                    article_link = f"https://zhuanlan.zhihu.com/p/{article_id}"
                    self.parse_zhihu_article(article_link)
                    self.save_processed_article(processed_filename, article_id)
                    progress_bar.update(1)  # 更新进度条

                elif item["type"] == "answer":
                    answer_id = str(item["id"])
                    if answer_id in processed_articles:
                        continue

                    answer_link = f"https://www.zhihu.com/question/{item['question']['id']}/answer/{answer_id}"
                    self.judge_type(answer_link)
                    self.save_processed_article(processed_filename, answer_id)
                    progress_bar.update(1)

            if data["paging"]["is_end"]:
                break

            offset += 10

        progress_bar.close()  # 完成后关闭进度条
        os.remove(processed_filename)  # 删除已处理文章的ID文件
        return folder_name

```

### csdn-downloader_img.py

```python
import os
import urllib.parse

import requests
from bs4 import BeautifulSoup
from markdownify import markdownify as md
from urllib.parse import unquote, urlparse, parse_qs
from tqdm import tqdm

from util import insert_new_line, get_article_date, download_image, get_valid_filename


class CsdnParserLocal:
    def __init__(self, hexo_uploader=False):
        self.hexo_uploader = hexo_uploader  # 是否为 hexo 博客上传
        self.session = requests.Session()  # 创建会话
        # 用户代理
        self.user_agents = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"
        self.headers = {  # 请求头
            'User-Agent': self.user_agents,
            'Accept-Language': 'en,zh-CN;q=0.9,zh;q=0.8',
        }
        self.session.headers.update(self.headers)  # 更新会话的请求头
        self.soup = None  # 存储页面的 BeautifulSoup 对象

    def check_connect_error(self, target_link):
        """
        检查是否连接错误
        """
        try:
            response = self.session.get(target_link)
            response.raise_for_status()
        except requests.exceptions.HTTPError as err:
            print(f"HTTP error occurred: {err}")

        except requests.exceptions.RequestException as err:
            print(f"Error occurred: {err}")

        self.soup = BeautifulSoup(response.content, "html.parser")

    def judge_type(self, target_link):
        """
        判断url类型
        """
        if target_link.find("category") != -1:
            # 如果是专栏
            title = self.parse_column(target_link)

        else:
            # 如果是单篇文章
            title = self.parse_article(target_link)

        return title

    def save_and_transform(self, title_element, content_element, author, target_link, date=None):
        """
        转化并保存为 Markdown 格式文件
        """
        # 获取标题和内容
        if title_element is not None:
            title = title_element.text.strip()
        else:
            title = "Untitled"

        # 防止文件名称太长，加载不出图像
        # markdown_title = get_valid_filename(title[-20:-1])
        # 如果觉得文件名太怪不好管理，那就使用全名
        markdown_title = get_valid_filename(title)

        if date:
            markdown_title = f"({date}){markdown_title}_{author}"
        else:
            markdown_title = f"{markdown_title}_{author}"

        if content_element is not None:
            # 将 css 样式移除
            for style_tag in content_element.find_all("style"):
                style_tag.decompose()

            # 处理内容中的标题
            for header in content_element.find_all(['h1', 'h2', 'h3', 'h4', 'h5', 'h6']):
                header_level = int(header.name[1])  # 从标签名中获取标题级别（例如，'h2' -> 2）
                header_text = header.get_text(strip=True)  # 提取标题文本
                # 转换为 Markdown 格式的标题
                markdown_header = f"{'#' * header_level} {header_text}"
                insert_new_line(self.soup, header, 1)
                header.replace_with(markdown_header)

            # 处理回答中的图片
            for img in content_element.find_all("img"):
                if 'src' in img.attrs:
                    img_url = img.attrs['src']
                else:
                    continue

                img_name = urllib.parse.quote(os.path.basename(img_url))
                img_path = f"{markdown_title}/{img_name}"

                extensions = ['.jpg', '.png', '.gif']  # 可以在此列表中添加更多的图片格式

                # 如果图片链接中图片后缀后面还有字符串则直接截停
                for ext in extensions:
                    index = img_path.find(ext)
                    if index != -1:
                        img_path = img_path[:index + len(ext)]
                        break  # 找到第一个匹配的格式后就跳出循环

                img["src"] = img_path

                # 下载图片并保存到本地
                os.makedirs(os.path.dirname(img_path), exist_ok=True)
                download_image(img_url, img_path, self.session)

                # 在图片后插入换行符
                insert_new_line(self.soup, img, 1)

            # 在图例后面加上换行符
            for figcaption in content_element.find_all("figcaption"):
                insert_new_line(self.soup, figcaption, 2)

            # 处理链接
            for link in content_element.find_all("a"):
                if 'href' in link.attrs:
                    original_url = link.attrs['href']

                    # 解析并解码 URL
                    parsed_url = urlparse(original_url)
                    query_params = parse_qs(parsed_url.query)
                    target_url = query_params.get('target', [original_url])[
                        0]  # 使用原 URL 作为默认值
                    article_url = unquote(target_url)  # 解码 URL

                    # 如果没有 data-text 属性，则使用文章链接作为标题
                    if 'data-text' not in link.attrs:
                        article_title = article_url
                    else:
                        article_title = link.attrs['data-text']

                    markdown_link = f"[{article_title}]({article_url})"

                    link.replace_with(markdown_link)

            # 提取并存储数学公式
            math_formulas = []
            math_tags = []
            for math_span in content_element.select("span.ztext-math"):
                latex_formula = math_span['data-tex']
                # math_formulas.append(latex_formula)
                # math_span.replace_with("@@MATH@@")
                # 使用特殊标记标记位置
                if latex_formula.find("\\tag") != -1:
                    math_tags.append(latex_formula)
                    insert_new_line(self.soup, math_span, 1)
                    math_span.replace_with("@@MATH_FORMULA@@")
                else:
                    math_formulas.append(latex_formula)
                    math_span.replace_with("@@MATH@@")

            # 获取文本内容
            content = content_element.decode_contents().strip()
            # 转换为 markdown
            content = md(content)

            # 将特殊标记替换为 LaTeX 数学公式
            for formula in math_formulas:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH@@", "$" + "{% raw %}" + formula + "{% endraw %}" + "$", 1)
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find('$') != -1:
                        content = content.replace("@@MATH@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH@@", f"${formula}$", 1)

            for formula in math_tags:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH\_FORMULA@@",
                        "$$" + "{% raw %}" + formula + "{% endraw %}" + "$$",
                        1,
                    )
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find("$") != -1:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"$${formula}$$", 1)

        else:
            content = ""

        # 转化为 Markdown 格式
        if content:
            markdown = f"# {title}\n\n **Author:** [{author}]\n\n **Link:** [{target_link}]\n\n{content}"
        else:
            markdown = f"# {title}\n\n Content is empty."

        # 保存 Markdown 文件
        with open(f"{markdown_title}.md", "w", encoding="utf-8") as f:
            f.write(markdown)

        return markdown_title

    def parse_article(self, target_link):
        """
        解析知乎文章并保存为Markdown格式文件
        """
        self.check_connect_error(target_link)

        title_element = self.soup.select_one("h1.title-article")
        content_element = self.soup.select_one("div#content_views")

        date = get_article_date(self.soup, "div.bar-content")
        author = self.soup.select_one(
            'div.bar-content').find_all("a")[0].text.strip()

        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def load_processed_articles(self, filename):
        """
        从文件加载已处理文章的ID。
        """
        if not os.path.exists(filename):
            return set()
        with open(filename, 'r', encoding='utf-8') as file:
            return set(file.read().splitlines())

    def save_processed_article(self, filename, article_id):
        """
        将处理过的文章ID保存到文件。
        """
        with open(filename, 'a', encoding='utf-8') as file:
            file.write(article_id + '\n')

    def parse_column(self, target_link):
        """
        解析知乎专栏并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)

        # 将所有文章放在一个以专栏标题命名的文件夹中
        title = self.soup.text.split('-')[0].split('_')[0].strip()
        total_articles = int(self.soup.text.split(
            '文章数：')[-1].split('文章阅读量')[0].strip())  # 总文章数
        folder_name = get_valid_filename(title)
        os.makedirs(folder_name, exist_ok=True)
        os.chdir(folder_name)

        processed_filename = "csdn_processed_articles.txt"
        processed_articles = self.load_processed_articles(processed_filename)

        offset = 0
        total_parsed = 0

        # 计算已处理的文章数
        already_processed = len(processed_articles)

        # 初始化进度条，从已处理的文章数开始
        progress_bar = tqdm(total=total_articles,
                            initial=already_processed, desc="解析文章")

        ul_element = self.soup.find('ul', class_='column_article_list')
        for li in ul_element.find_all('li'):
            article_link = li.find('a')['href']
            article_id = article_link.split('/')[-1]
            if article_id in processed_articles:
                continue

            self.parse_article(article_link)
            self.save_processed_article(processed_filename, article_id)
            progress_bar.update(1)  # 更新进度条

        progress_bar.close()  # 完成后关闭进度条
        os.remove(processed_filename)  # 删除已处理文章的ID文件
        return folder_name

class CsdnParser:
    def __init__(self, hexo_uploader=False):
        self.hexo_uploader = hexo_uploader  # 是否为 hexo 博客上传
        self.session = requests.Session()  # 创建会话
        # 用户代理
        self.user_agents = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"
        self.headers = {  # 请求头
            'User-Agent': self.user_agents,
            'Accept-Language': 'en,zh-CN;q=0.9,zh;q=0.8',
        }
        self.session.headers.update(self.headers)  # 更新会话的请求头
        self.soup = None  # 存储页面的 BeautifulSoup 对象

    def check_connect_error(self, target_link):
        """
        检查是否连接错误
        """
        try:
            response = self.session.get(target_link)
            response.raise_for_status()
        except requests.exceptions.HTTPError as err:
            print(f"HTTP error occurred: {err}")

        except requests.exceptions.RequestException as err:
            print(f"Error occurred: {err}")

        self.soup = BeautifulSoup(response.content, "html.parser")

    def judge_type(self, target_link):
        """
        判断url类型
        """
        if target_link.find("category") != -1:
            # 如果是专栏
            title = self.parse_column(target_link)

        else:
            # 如果是单篇文章
            title = self.parse_article(target_link)

        return title

    def save_and_transform(self, title_element, content_element, author, target_link, date=None):
        """
        转化并保存为 Markdown 格式文件
        """
        # 获取标题和内容
        if title_element is not None:
            title = title_element.text.strip()
        else:
            title = "Untitled"

        # 防止文件名称太长，加载不出图像
        # markdown_title = get_valid_filename(title[-20:-1])
        # 如果觉得文件名太怪不好管理，那就使用全名
        markdown_title = get_valid_filename(title)

        if date:
            markdown_title = f"({date}){markdown_title}_{author}"
        else:
            markdown_title = f"{markdown_title}_{author}"

        if content_element is not None:
            # 将 css 样式移除
            for style_tag in content_element.find_all("style"):
                style_tag.decompose()

            # 处理内容中的标题
            for header in content_element.find_all(['h1', 'h2', 'h3', 'h4', 'h5', 'h6']):
                header_level = int(header.name[1])  # 从标签名中获取标题级别（例如，'h2' -> 2）
                header_text = header.get_text(strip=True)  # 提取标题文本
                # 转换为 Markdown 格式的标题
                markdown_header = f"{'#' * header_level} {header_text}"
                insert_new_line(self.soup, header, 1)
                header.replace_with(markdown_header)

                # 处理回答中的图片
                for figure in content_element.find_all("figure"):
                    img = figure.find("img")
                    if img and 'src' in img.attrs:
                        img_url = img.attrs['src']

                        # 提取 figcaption 内容
                        figcaption = figure.find("figcaption")
                        figcaption_text = figcaption.get_text(strip=True) if figcaption else "Image"

                        # 替换 img 标签为 Markdown 图片格式, 使用 figcaption 内容作为描述
                        markdown_img = f"![{figcaption_text}]({img_url})"

                        # 在 img 后插入 Markdown 格式字符串
                        img.insert_after(markdown_img)
                        img.extract()  # 移除 img 标签

                        # 若存在 figcaption，移除它
                        if figcaption:
                            figcaption.extract()

                        # 在插入的 Markdown 图片后插入换行符
                        next_sibling = img.find_next_sibling()
                        if next_sibling is not None:
                            insert_new_line(self.soup, next_sibling, 1)
                        else:
                            # 如果没有下一个兄弟元素，可以选择在内容末尾插入换行符
                            insert_new_line(self.soup, content_element, 1)  # 或者一个合适的元素

            # 处理链接
            for link in content_element.find_all("a"):
                if 'href' in link.attrs:
                    original_url = link.attrs['href']

                    # 解析并解码 URL
                    parsed_url = urlparse(original_url)
                    query_params = parse_qs(parsed_url.query)
                    target_url = query_params.get('target', [original_url])[
                        0]  # 使用原 URL 作为默认值
                    article_url = unquote(target_url)  # 解码 URL

                    # 如果没有 data-text 属性，则使用文章链接作为标题
                    if 'data-text' not in link.attrs:
                        article_title = article_url
                    else:
                        article_title = link.attrs['data-text']

                    markdown_link = f"[{article_title}]({article_url})"

                    link.replace_with(markdown_link)

            # 提取并存储数学公式
            math_formulas = []
            math_tags = []
            for math_span in content_element.select("span.ztext-math"):
                latex_formula = math_span['data-tex']
                # math_formulas.append(latex_formula)
                # math_span.replace_with("@@MATH@@")
                # 使用特殊标记标记位置
                if latex_formula.find("\\tag") != -1:
                    math_tags.append(latex_formula)
                    insert_new_line(self.soup, math_span, 1)
                    math_span.replace_with("@@MATH_FORMULA@@")
                else:
                    math_formulas.append(latex_formula)
                    math_span.replace_with("@@MATH@@")

            # 获取文本内容
            content = content_element.decode_contents().strip()
            # 转换为 markdown
            content = md(content)

            # 将特殊标记替换为 LaTeX 数学公式
            for formula in math_formulas:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH@@", "$" + "{% raw %}" + formula + "{% endraw %}" + "$", 1)
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find('$') != -1:
                        content = content.replace("@@MATH@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH@@", f"${formula}$", 1)

            for formula in math_tags:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH\_FORMULA@@",
                        "$$" + "{% raw %}" + formula + "{% endraw %}" + "$$",
                        1,
                    )
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find("$") != -1:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"$${formula}$$", 1)

        else:
            content = ""

        # 转化为 Markdown 格式
        if content:
            markdown = f"# {title}\n\n **Author:** [{author}]\n\n **Link:** [{target_link}]\n\n{content}"
        else:
            markdown = f"# {title}\n\n Content is empty."

        # 保存 Markdown 文件
        with open(f"{markdown_title}.md", "w", encoding="utf-8") as f:
            f.write(markdown)

        return markdown_title

    def parse_article(self, target_link):
        """
        解析知乎文章并保存为Markdown格式文件
        """
        self.check_connect_error(target_link)

        title_element = self.soup.select_one("h1.title-article")
        content_element = self.soup.select_one("div#content_views")

        date = get_article_date(self.soup, "div.bar-content")
        author = self.soup.select_one(
            'div.bar-content').find_all("a")[0].text.strip()

        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def load_processed_articles(self, filename):
        """
        从文件加载已处理文章的ID。
        """
        if not os.path.exists(filename):
            return set()
        with open(filename, 'r', encoding='utf-8') as file:
            return set(file.read().splitlines())

    def save_processed_article(self, filename, article_id):
        """
        将处理过的文章ID保存到文件。
        """
        with open(filename, 'a', encoding='utf-8') as file:
            file.write(article_id + '\n')

    def parse_column(self, target_link):
        """
        解析知乎专栏并保存为 Markdown 格式文件
        """
        self.check_connect_error(target_link)

        # 将所有文章放在一个以专栏标题命名的文件夹中
        title = self.soup.text.split('-')[0].split('_')[0].strip()
        total_articles = int(self.soup.text.split(
            '文章数：')[-1].split('文章阅读量')[0].strip())  # 总文章数
        folder_name = get_valid_filename(title)
        os.makedirs(folder_name, exist_ok=True)
        os.chdir(folder_name)

        processed_filename = "csdn_processed_articles.txt"
        processed_articles = self.load_processed_articles(processed_filename)

        offset = 0
        total_parsed = 0

        # 计算已处理的文章数
        already_processed = len(processed_articles)

        # 初始化进度条，从已处理的文章数开始
        progress_bar = tqdm(total=total_articles,
                            initial=already_processed, desc="解析文章")

        ul_element = self.soup.find('ul', class_='column_article_list')
        for li in ul_element.find_all('li'):
            article_link = li.find('a')['href']
            article_id = article_link.split('/')[-1]
            if article_id in processed_articles:
                continue

            self.parse_article(article_link)
            self.save_processed_article(processed_filename, article_id)
            progress_bar.update(1)  # 更新进度条

        progress_bar.close()  # 完成后关闭进度条
        os.remove(processed_filename)  # 删除已处理文章的ID文件
        return folder_name

```
### weixin-downloader_img.py

```python
import os
import urllib.parse

import requests
from bs4 import BeautifulSoup
from markdownify import markdownify as md
from urllib.parse import unquote, urlparse, parse_qs
from util import insert_new_line, process_markdown_content, download_image, get_valid_filename, get_article_date_weixin


class WeixinParserLocal:
    def __init__(self, hexo_uploader=False):
        self.hexo_uploader = hexo_uploader  # 是否为 hexo 博客上传
        self.session = requests.Session()  # 创建会话
        # 用户代理
        self.user_agents = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"
        self.headers = {  # 请求头
            'User-Agent': self.user_agents,
            'Accept-Language': 'en,zh-CN;q=0.9,zh;q=0.8',
        }
        self.session.headers.update(self.headers)  # 更新会话的请求头
        self.soup = None  # 存储页面的 BeautifulSoup 对象

    def check_connect_error(self, target_link):
        """
        检查是否连接错误
        """
        try:
            response = self.session.get(target_link)
            response.raise_for_status()
        except requests.exceptions.HTTPError as err:
            print(f"HTTP error occurred: {err}")

        except requests.exceptions.RequestException as err:
            print(f"Error occurred: {err}")

        self.soup = BeautifulSoup(response.content, "html.parser")

    def judge_type(self, target_link):
        """
        判断url类型
        """
        title = self.parse_article(target_link)

        return title

    def save_and_transform(self, title_element, content_element, author, target_link, date=None):
        """
        转化并保存为 Markdown 格式文件
        """
        # 获取标题和内容
        if title_element is not None:
            title = title_element.text.strip()
        else:
            title = "Untitled"

        # 防止文件名称太长，加载不出图像
        # markdown_title = get_valid_filename(title[-20:-1])
        # 如果觉得文件名太怪不好管理，那就使用全名
        markdown_title = get_valid_filename(title)

        if date:
            markdown_title = f"({date}){markdown_title}_{author}"
        else:
            markdown_title = f"{markdown_title}_{author}"

        if content_element is not None:
            # 将 css 样式移除
            for style_tag in content_element.find_all("style"):
                style_tag.decompose()

            # 处理内容中的标题
            for header in content_element.find_all(['h1', 'h2', 'h3', 'h4', 'h5', 'h6']):
                header_level = int(header.name[1])  # 从标签名中获取标题级别（例如，'h2' -> 2）
                header_text = header.get_text(strip=True)  # 提取标题文本
                # 转换为 Markdown 格式的标题
                markdown_header = f"{'#' * header_level} {header_text}"
                insert_new_line(self.soup, header, 1)
                header.replace_with(markdown_header)

            img_index = 0
            # 处理回答中的图片
            for img in content_element.find_all("img"):
                if 'data-src' in img.attrs:
                    img_url = img.attrs['data-src']
                elif 'src' in img.attrs:
                    img_url = img.attrs['src']
                else:
                    continue

                # 解析URL并获取查询参数
                parsed_url = urllib.parse.urlparse(img_url)
                query_params = urllib.parse.parse_qs(parsed_url.query)

                # 确定图片扩展名，优先从查询参数中获取
                if 'wx_fmt' in query_params:
                    ext = f".{query_params['wx_fmt'][0]}"
                else:
                    # 如果没有查询参数，则尝试从路径部分获取扩展名
                    ext = os.path.splitext(parsed_url.path)[1] or '.jpg'  # 默认使用.jpg

                # 提取图片格式
                img_name = f"img_{img_index:02d}{ext}"
                img_path = f"{markdown_title}/{img_name}"

                extensions = ['.jpg', '.jpeg', '.png',
                              '.gif']  # 可以在此列表中添加更多的图片格式

                # 如果图片链接中图片后缀后面还有字符串则直接截停
                for ext in extensions:
                    index = img_path.find(ext)
                    if index != -1:
                        img_path = img_path[:index + len(ext)]
                        break  # 找到第一个匹配的格式后就跳出循环

                img["src"] = img_path

                # 下载图片并保存到本地
                os.makedirs(os.path.dirname(img_path), exist_ok=True)
                download_image(img_url, img_path, self.session)

                img_index += 1

                # 在图片后插入换行符
                insert_new_line(self.soup, img, 1)

            # 在图例后面加上换行符
            for figcaption in content_element.find_all("figcaption"):
                insert_new_line(self.soup, figcaption, 2)

            # 处理链接
            for link in content_element.find_all("a"):
                if 'href' in link.attrs:
                    original_url = link.attrs['href']

                    # 解析并解码 URL
                    parsed_url = urlparse(original_url)
                    query_params = parse_qs(parsed_url.query)
                    target_url = query_params.get('target', [original_url])[
                        0]  # 使用原 URL 作为默认值
                    article_url = unquote(target_url)  # 解码 URL

                    # 如果没有 data-text 属性，则使用文章链接作为标题
                    if 'data-text' not in link.attrs:
                        article_title = article_url
                    else:
                        article_title = link.attrs['data-text']

                    markdown_link = f"[{article_title}]({article_url})"

                    link.replace_with(markdown_link)

            # 提取并存储数学公式
            math_formulas = []
            math_tags = []
            for math_span in content_element.select("span.ztext-math"):
                latex_formula = math_span['data-tex']
                # math_formulas.append(latex_formula)
                # math_span.replace_with("@@MATH@@")
                # 使用特殊标记标记位置
                if latex_formula.find("\\tag") != -1:
                    math_tags.append(latex_formula)
                    insert_new_line(self.soup, math_span, 1)
                    math_span.replace_with("@@MATH_FORMULA@@")
                else:
                    math_formulas.append(latex_formula)
                    math_span.replace_with("@@MATH@@")

            # 获取文本内容
            content = content_element.decode_contents().strip()
            # 转换为 markdown
            content = md(content)

            # 将特殊标记替换为 LaTeX 数学公式
            for formula in math_formulas:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH@@", "$" + "{% raw %}" + formula + "{% endraw %}" + "$", 1)
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find('$') != -1:
                        content = content.replace("@@MATH@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH@@", f"${formula}$", 1)

            for formula in math_tags:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH\_FORMULA@@",
                        "$$" + "{% raw %}" + formula + "{% endraw %}" + "$$",
                        1,
                    )
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find("$") != -1:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"$${formula}$$", 1)

        else:
            content = ""

        # 转化为 Markdown 格式
        if content:
            markdown = f"# {title}\n\n **Author:** [{author}]\n\n **Link:** [{target_link}]\n\n{content}"
        else:
            markdown = f"# {title}\n\n Content is empty."

        # 保存 Markdown 文件
        with open(f"{markdown_title}.md", "w", encoding="utf-8") as f:
            f.write(markdown)

        return markdown_title

    def parse_article(self, target_link):
        """
        解析知乎文章并保存为Markdown格式文件
        """
        self.check_connect_error(target_link)

        title_element = self.soup.select_one("h1#activity-name")
        content_element = self.soup.select_one("div#js_content")

        date = get_article_date_weixin(self.soup.find_all('script', type='text/javascript'))
        author = self.soup.select_one("div#meta_content").find_all("a")[
            0].text.strip()

        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def load_processed_articles(self, filename):
        """
        从文件加载已处理文章的ID。
        """
        if not os.path.exists(filename):
            return set()
        with open(filename, 'r', encoding='utf-8') as file:
            return set(file.read().splitlines())

    def save_processed_article(self, filename, article_id):
        """
        将处理过的文章ID保存到文件。
        """
        with open(filename, 'a', encoding='utf-8') as file:
            file.write(article_id + '\n')

class WeixinParser:
    def __init__(self, hexo_uploader=False):
        self.hexo_uploader = hexo_uploader  # 是否为 hexo 博客上传
        self.session = requests.Session()  # 创建会话
        # 用户代理
        self.user_agents = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"
        self.headers = {  # 请求头
            'User-Agent': self.user_agents,
            'Accept-Language': 'en,zh-CN;q=0.9,zh;q=0.8',
        }
        self.session.headers.update(self.headers)  # 更新会话的请求头
        self.soup = None  # 存储页面的 BeautifulSoup 对象

    def check_connect_error(self, target_link):
        """
        检查是否连接错误
        """
        try:
            response = self.session.get(target_link)
            response.raise_for_status()
        except requests.exceptions.HTTPError as err:
            print(f"HTTP error occurred: {err}")

        except requests.exceptions.RequestException as err:
            print(f"Error occurred: {err}")

        self.soup = BeautifulSoup(response.content, "html.parser")

    def judge_type(self, target_link):
        """
        判断url类型
        """
        title = self.parse_article(target_link)

        return title

    def save_and_transform(self, title_element, content_element, author, target_link, date=None):
        """
        转化并保存为 Markdown 格式文件
        """
        # 获取标题和内容
        if title_element is not None:
            title = title_element.text.strip()
        else:
            title = "Untitled"

        # 防止文件名称太长，加载不出图像
        # markdown_title = get_valid_filename(title[-20:-1])
        # 如果觉得文件名太怪不好管理，那就使用全名
        markdown_title = get_valid_filename(title)

        if date:
            markdown_title = f"({date}){markdown_title}_{author}"
        else:
            markdown_title = f"{markdown_title}_{author}"

        if content_element is not None:
            # 将 css 样式移除
            for style_tag in content_element.find_all("style"):
                style_tag.decompose()

            # 处理内容中的标题
            for header in content_element.find_all(['h1', 'h2', 'h3', 'h4', 'h5', 'h6']):
                header_level = int(header.name[1])  # 从标签名中获取标题级别（例如，'h2' -> 2）
                header_text = header.get_text(strip=True)  # 提取标题文本
                # 转换为 Markdown 格式的标题
                markdown_header = f"{'#' * header_level} {header_text}"
                insert_new_line(self.soup, header, 1)
                header.replace_with(markdown_header)

            img_index = 0
            # 处理回答中的图片
            for img in content_element.find_all("img"):
                if 'data-src' in img.attrs:
                    img_url = img.attrs['data-src']
                elif 'src' in img.attrs:
                    img_url = img.attrs['src']
                else:
                    continue

                # 替换 img 标签为 Markdown 图片格式, 使用 figcaption 内容作为描述
                markdown_img = f"![Image]({img_url})"

                # 在 img 后插入 Markdown 格式字符串
                img.insert_after(markdown_img)
                img.extract()  # 移除 img 标签

                # 在插入的 Markdown 图片后插入换行符
                next_sibling = img.find_next_sibling()
                if next_sibling is not None:
                    insert_new_line(self.soup, next_sibling, 1)
                else:
                    # 如果没有下一个兄弟元素，可以选择在内容末尾插入换行符
                    insert_new_line(self.soup, content_element, 1)  # 或者一个合适的元素

            # 在图例后面加上换行符
            for figcaption in content_element.find_all("figcaption"):
                insert_new_line(self.soup, figcaption, 2)
            # 处理链接
            for link in content_element.find_all("a"):
                if 'href' in link.attrs:
                    original_url = link.attrs['href']

                    # 解析并解码 URL
                    parsed_url = urlparse(original_url)
                    query_params = parse_qs(parsed_url.query)
                    target_url = query_params.get('target', [original_url])[
                        0]  # 使用原 URL 作为默认值
                    article_url = unquote(target_url)  # 解码 URL

                    # 如果没有 data-text 属性，则使用文章链接作为标题
                    if 'data-text' not in link.attrs:
                        article_title = article_url
                    else:
                        article_title = link.attrs['data-text']

                    markdown_link = f"[{article_title}]({article_url})"

                    link.replace_with(markdown_link)

            # 提取并存储数学公式
            math_formulas = []
            math_tags = []
            for math_span in content_element.select("span.ztext-math"):
                latex_formula = math_span['data-tex']
                # math_formulas.append(latex_formula)
                # math_span.replace_with("@@MATH@@")
                # 使用特殊标记标记位置
                if latex_formula.find("\\tag") != -1:
                    math_tags.append(latex_formula)
                    insert_new_line(self.soup, math_span, 1)
                    math_span.replace_with("@@MATH_FORMULA@@")
                else:
                    math_formulas.append(latex_formula)
                    math_span.replace_with("@@MATH@@")

            # 获取文本内容
            content = content_element.decode_contents().strip()
            # 转换为 markdown
            content = md(content)

            # 将特殊标记替换为 LaTeX 数学公式
            for formula in math_formulas:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH@@", "$" + "{% raw %}" + formula + "{% endraw %}" + "$", 1)
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find('$') != -1:
                        content = content.replace("@@MATH@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH@@", f"${formula}$", 1)

            for formula in math_tags:
                if self.hexo_uploader:
                    content = content.replace(
                        "@@MATH\_FORMULA@@",
                        "$$" + "{% raw %}" + formula + "{% endraw %}" + "$$",
                        1,
                    )
                else:
                    # 如果公式中包含 $ 则不再添加 $ 符号
                    if formula.find("$") != -1:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"{formula}", 1)
                    else:
                        content = content.replace(
                            "@@MATH\_FORMULA@@", f"$${formula}$$", 1)

        else:
            content = ""

        # 转化为 Markdown 格式
        if content:
            markdown = f"# {title}\n\n **Author:** [{author}]\n\n **Link:** [{target_link}]\n\n{content}"
        else:
            markdown = f"# {title}\n\n Content is empty."

        # 保存 Markdown 文件
        markdown = process_markdown_content(markdown)
        with open(f"{markdown_title}.md", "w", encoding="utf-8") as f:
            f.write(markdown)

        return markdown_title

    def parse_article(self, target_link):
        """
        解析知乎文章并保存为Markdown格式文件
        """
        self.check_connect_error(target_link)

        title_element = self.soup.select_one("h1#activity-name")
        content_element = self.soup.select_one("div#js_content")

        date = get_article_date_weixin(self.soup.find_all('script', type='text/javascript'))
        author = self.soup.select_one("div#meta_content").find_all("a")[
            0].text.strip()

        markdown_title = self.save_and_transform(
            title_element, content_element, author, target_link, date)

        return markdown_title

    def load_processed_articles(self, filename):
        """
        从文件加载已处理文章的ID。
        """
        if not os.path.exists(filename):
            return set()
        with open(filename, 'r', encoding='utf-8') as file:
            return set(file.read().splitlines())

    def save_processed_article(self, filename, article_id):
        """
        将处理过的文章ID保存到文件。
        """
        with open(filename, 'a', encoding='utf-8') as file:
            file.write(article_id + '\n')
```



## 参考资料

[知乎专栏文章 Markdown 转换器](https://github.com/chenluda/zhihu-download)

[代码 | 将知乎专栏文章转换为 Markdown 文件保存到本地](https://zhuanlan.zhihu.com/p/622601955)








