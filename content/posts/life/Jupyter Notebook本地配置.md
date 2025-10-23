---
title: "Jupyter Notebook本地配置"
date: 2023-11-18T18:34:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
categories:
- 工具包
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

# 安装

在cmd中输入`pip install -i https://pypi.douban.com/simple/ jupyter`

# 如何更改Jupyter Notebook的默认工作路径？

1.在cmd中输入命令`jupyter notebook --generate-config`使Jupyter产生配置文件：Jupyter_notebook_config.py

2.在 C:\Users\Administrator\.jupyter 找到刚刚生成的配置文件 jupyter_notebook_config.py

[![](https://img2020.cnblogs.com/blog/1664108/202109/1664108-20210917153532026-690575438.png)](https://img2020.cnblogs.com/blog/1664108/202109/1664108-20210917153532026-690575438.png)

3.用记事本打开此配置文档，并用搜索（Ctrl+F）找到如下字段：# c.ServerApp.root_dir ，在后面的引号“”中输入想修改为的默认工作路径，删除前面的#，保存文件

改为如下内容：

```
## The directory to use for notebooks and kernels.  
#  Default: ''  
c.ServerApp.root_dir = 'E:\\notebook'
```

# 高级用法

[来源](https://blog.csdn.net/red_stone1/article/details/72863749)

## **单元操作**

当你在编辑notebook时，你希望使用更多高级的cell操作。幸运的是，notebook允许你使用非常丰富的cell操作。你可以删除一个cell，先选中cell，点击Edit->Delete cell。你也可以移动一个cell的位置，点击`Edit->  Move cell [up | down]`。你也可以剪切、粘贴cell，点击Edit->Cut Cell then Edit -> Paste Cell …，选择需要的粘贴形式。如果有许多cells，而你只想执行一次，或者你想一次性执行大量代码，你就可以合并多个cells，点击`Edit->Merge cell [above|below]`。编辑notebook时，记住这些操作，会节约你很多时间。

## 集成图片

让我们再深入地探讨下markdown单元类型，即便它的类型是markdown，它同时也支持HTML代码。你可以在你的cell中创建更高级的样式，比如添加图片等等。举个例子来说，如果你想在notebook中添加Jupyter的图标，尺寸为100x100，并且放置在cell左侧，可以这样编写：

```html
<img src="http://blog.jupyter.org/content/images/2015/02/jupyter-sq-text.png"
style="width:100px;height:100px;float:left">
```

运行该单元，效果如下：

![这里写图片描述](https://img-blog.csdn.net/20170605082511967?)

## 集成数学公式

除此之外，markdown还支持LaTex语法。你可以在markdown cell中按照LaTex语法规则写下方程式，然后直接运行，就可以看到结果。例如运行下面方程式：

```latex
$$\int_0^{+\infty} x^2 dx$$
```

运行后就得到了LaTex方程式：

![这里写图片描述](https://img-blog.csdn.net/20170605083006316?)

## **导出功能**

notebook另一个强大的功能就是导出功能。你可以把你的notebook（例如是个图解代码课程）导出为如下多种形式：

- HTML
- Markdown
- ReST
- PDF(Through LaTex)
- Raw Python

如果导出成PDF格式，你甚至可以不使用LaTex就创建了一个漂亮的文档。或者，你可以将你的notebook保存为HTML格式，发布到个人网站上。你还可以导出成ReST格式，作为软件库的文档。

## **集成Matplotlib**

如果你用Python画过图，应该知道matplotlib。Matplotlib是用来画图的Python库。与Jupyter notebook结合使用时，效果更好。下面，让我们来看看如何在Jupyter notebook中使用matplotlib。

为了在Jupyter notebook中使用matplotlib，你需要告诉Jupyter获取所有matplotlib生成的图形，并把它们全部嵌入到notebook中。为此，只需输入以下命令：

```bash
%matplotlib inline
```

这条语句执行可能耗费几秒钟，但是只需要你打开notebook时执行一次就好。让我们作个图，看看是怎么集成的：

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(20)
y = x**2

plt.plot(x, y)
```

这段简单代码将绘出y=x^2对应的二次曲线。运行这个cell，结果如下所示：

![这里写图片描述](https://img-blog.csdn.net/20170605085947890?)

我们可以看到，图直接嵌入到notebook中，就在代码下面。修改代码，重新运行，图形将自动同步更新。对于每个想要把代码和图形放在同一个文件中的数据科学家来说，这是一个很好的特性，这样可以清楚知道每段代码究竟干了什么。同时，在文档中添加一些文字型描述也有很大的作用。

##### **非本地内核**

Jupyter notebook非常容易从本地电脑上启动，也允许多个人通过网络连接到同一个Jupyter实例。你是否注意到，在上一部分的教程中，启动Jupyter时出现了下面这条语句：

IPython Notebook运行在：[http://localhost:8888/](http://localhost:8888/)

这条语句表示你的notebook是本地运行，可以在浏览器中输入地址[http://localhost:8888/](http://localhost:8888/)，打开你的notebook。通过修改配置，可以让notebook面向公开访问。这样，任何人如果知道这个notebook地址，就通过浏览器可以远程访问并修改notebook。

# 如何将ipynb转换为html，md，pdf等格式

[来源](https://blog.csdn.net/red_stone1/article/details/73380517)

那么用jupyter notebook写的后缀名是.ipynb的文件如何转换成html，md，pdf等格式呢？本文将做简单介绍。

## ipynb转为html格式

在Ubuntu命令行输入：

`jupyter nbconvert --to html notebook.ipynb`

另外，jupyter提供了一些命令，可以对生成的html格式进行配置：

`jupyter nbconvert --to html --template full notebook.ipynb`

这是默认配置，提供完整的静态html格式，交互性更强。

`jupyter nbconvert --to html --template basic notebook.ipynb`

简化的html，用于嵌入网页、博客等，这不包括html标题。

## ipynb转换为md格式

在Ubuntu命令行输入：

`jupyter nbconvert --to md notebook.ipynb`

简单的Markdown格式输出，cell单元不受影响，代码cell缩进4个空格。

## ipynb转换为tex格式

在Ubuntu命令行输入：

`jupyter nbconvert --to letex notebook.ipynb`

Letex导出格式，生成后缀名为NOTEBOOK_NAME.tex的文件。jupyter提供的额外模板配置为：

`jupyter nbconvert --to letex -template article notebook.ipynb`

这是默认配置，Latex文章。

`jupyter nbconvert --to letex -template report notebook.ipynb`

Latex报告，提供目录和章节。

`jupyter nbconvert --to letex -template basic notebook.ipynb`

最基本的Latex输出，经常用来自定义配置。

## ipython转换为pdf格式

在Ubuntu命令行输入：

`jupyter nbconvert --to pdf notebook.ipynb`

转换为pdf格式分模板配置与latex配置是一样的。但是直接转换为pdf格式经常会出现错误500: Internal Server Error

该错误提示没有安装xelatex。所以，我们需要提前安装xelatex，方法是安装texLive套装：

`sudo apt-get install texlive-full`

texlive-full的安装包有点大，约1G多。

## 简单的转换方法

ipynb转换为html、md、pdf等格式，还有另一种更简单的方法：在jupyter notebook中，选择File->Download as，直接选择需要转换的格式就可以了。需要注意的是，转换为pdf格式之前，同样要保证已经安装了xelatex。









