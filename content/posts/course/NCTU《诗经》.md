---
title: "NCTU《诗经》"
date: 2024-09-05T18:34:25+08:00
lastmod: 2024-09-05T22:54:22+08:00
math: true
categories:
- 在线课程
- 文学
- 儒学
tags:
- 诗经
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


# 台湾交通大学《诗经》

## 前言

《诗经》内容过大繁杂，这篇博文只是做个记录，具体的《诗经》仓库还没丰富起来。

BV1Hs411B7w1

## 简介

《诗经》由台湾交通大学教授刘龙勋先生讲授。

## 优缺点

优点：资料详实，有独立见解

缺点：把公侯称为皇帝，把邦小君成为皇后，确实不太对头~


## 课程目录

### P1 01课程简介 18:50
### P2 02历代诗经学（一） 1:13:36
### P3 03历代诗经学（二） 1:34:50
### P4 04历代诗经学（三） 1:38:17
### P5 05历代诗经学（四） 1:23:50
### P6 06二南 关雎 1:35:42
### P7 07关雎 葛覃 1:33:51
### P8 08葛覃 卷耳 1:31:19
### P9 09樛木 螽斯 桃夭 1:29:10
### P10 10桃夭 兔罝 芣苢 汉广 1:31:57
### P11 11汉广 鹊巢 采苹 1:34:23
### P12 12采苹 甘棠 羔羊 摽有梅 1:27:34
### P13 13小星 江有汜 野有死麕 1:34:41
### P14 14野有死麕 何彼穠矣 騶虞 柏舟 1:34:23
### P15 15凯风 匏有苦叶 谷风 1:33:52
### P16 16谷风 静女 新台 二子乘舟 柏舟 1:26:38
### P17 17桑中 相鼠 载驰 淇奥 1:30:00
### P18 18淇奥 硕人 氓 伯兮 1:39:36

## 浏览器控制台提取 B 站视频合集各集内容

[JavaScript获取B站分集视频标题及各集时长、累计时长](https://blog.csdn.net/weixin_42467340/article/details/122470953)

控制台提取指令如下所示：

```js
var box=document.getElementsByClassName('list-box')[0];
var boxtext=box.innerText;
var textline=boxtext.replace(/\n(?!P\d+)/g,' ');
console.log(textline);
```

## 抓取 CTEXT 上的《诗经》内容

### Python 脚本

```python
from bs4 import BeautifulSoup
import requests

headers = {
    "User-Agent" : "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36 Edg/127.0.0.0"
}

def getText(url):
    print(url)
    response = requests.get(url, headers=headers)
    response.encoding = 'utf-8'
    #print(type(response)) <class 'requests.models.Response'>
    #print(type(response.text)) <class 'str'>
    # 给定的HTML文本
    html_content = response.text
    # 解析HTML
    soup = BeautifulSoup(html_content, 'html.parser')

    # 提取标题和诗句
    titles = []
    result = []

    # 提取所有的标题

    for h2 in soup.find_all('h2'):
        title = h2.get_text()
        titles.append(title)
    print(titles)

    # 提取相关的诗句
    for tr in soup.find_all('tr'):
        ctext = tr.find_all('td', class_='ctext')
        if ctext:
            for text in ctext:
                #print("文本内容")
                #print(text)
                #print(text.find_all(string=True))
                # 取出文本内容，去除其他HTML标签
                cleaned_text = ''.join(text.find_all(string=True)).replace('\n', '').strip()
                if(len(cleaned_text) <= 6):
                    cleaned_text = cleaned_text[:-1]
                    cleaned_text = "## " + cleaned_text + "\n"
                else:
                    cleaned_text = "**" + cleaned_text + "**\n"
                result.append(cleaned_text)
                #print("清理后文本内容")
                #print(cleaned_text)


    # 替换<br />为换行符
    final_output = []
    for item in result:
        item = item.replace('<br />', '\n')
        final_output.append(item)

    # 打印结果，确保只有一个《葛覃》
    final_output = [final_output[0]] + final_output[1:]  # 只保留一个标题
    final_output = list(dict.fromkeys(final_output))  # 移除重复内容
    with open( str(titles[0]) + ".md", mode='w', encoding="utf-8") as f:
        header = "# " + str(titles[0]) + "\n"
        print(header)
        f.write(header)
        for line in final_output:
            f.write(line)
        
#import os
#print(os.getcwd())

with open("urls.txt", "r") as f:
    for line in f.readlines():
        #print(line)
        line = line.strip("\n")
        if line != "\n":
            getText(line)
```

### urls.txt

```txt
https://ctext.org/book-of-poetry/odes-of-zhou-and-the-south/zh
https://ctext.org/book-of-poetry/odes-of-shao-and-the-south/zh
https://ctext.org/book-of-poetry/odes-of-bei/zh
https://ctext.org/book-of-poetry/odes-of-yong/zh
https://ctext.org/book-of-poetry/odes-of-wei/zh
https://ctext.org/book-of-poetry/odes-of-wang/zh
https://ctext.org/book-of-poetry/odes-of-zheng/zh
https://ctext.org/book-of-poetry/odes-of-qi/zh
https://ctext.org/book-of-poetry/odes-of-wei1/zh
https://ctext.org/book-of-poetry/odes-of-tang/zh
https://ctext.org/book-of-poetry/odes-of-qin/zh
https://ctext.org/book-of-poetry/odes-of-chen/zh
https://ctext.org/book-of-poetry/odes-of-gui/zh
https://ctext.org/book-of-poetry/odes-of-cao/zh
https://ctext.org/book-of-poetry/odes-of-bin/zh
https://ctext.org/book-of-poetry/decade-of-lu-ming/zh
https://ctext.org/book-of-poetry/decade-of-baihua/zh
https://ctext.org/book-of-poetry/decade-of-tong-gong/zh
https://ctext.org/book-of-poetry/decade-of-qi-fu/zh
https://ctext.org/book-of-poetry/decade-of-xiao-min/zh
https://ctext.org/book-of-poetry/decade-of-bei-shan/zh
https://ctext.org/book-of-poetry/decade-of-sang-hu/zh
https://ctext.org/book-of-poetry/decade-of-du-ren-shi/zh
https://ctext.org/book-of-poetry/decade-of-wen-wang/zh
https://ctext.org/book-of-poetry/decade-of-sheng-min/zh
https://ctext.org/book-of-poetry/decade-of-dang/zh
https://ctext.org/book-of-poetry/sacrificial-odes-of-zhou/zh
https://ctext.org/book-of-poetry/decade-of-qing-miao/zh
https://ctext.org/book-of-poetry/decade-of-chen-gong/zh
https://ctext.org/book-of-poetry/decade-of-min-yu-xiao-zi/zh
https://ctext.org/book-of-poetry/praise-odes-of-lu/zh
https://ctext.org/book-of-poetry/sacrificial-odes-of-shang/zh
```







