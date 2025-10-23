---
title: "用pdfjs在线预览pdf书籍教程"
date: 2023-05-29T13:34:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
categories:
- 豫游之乐
- Getting Started
tags:
- pdfjs
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

我打算做数学、物理等的教程便于自己将来阅读，但是上传latex公式和各种图像比较费时费力，于是乎我想到用图片来解决这个问题。然而，用typora结合picgo往github仓库里面上传图片总会有很多图片上传失败，而且图片过多影响博客加载速度，让我很受打击。睡前想到可以用在线pdf阅读的方式来进行这项事业，我于是第二天把准备好的图片先转成pdf文件，然后把pdf文件上传到github仓库，再通过开启github pages的功能获得在线预览的URL实现文件在线阅读。

加载时间过长可以通过边加载边渲染的方式进行，不过这实现难度有点高，我选择了用cdnjs库来加速加载过程。虽然这样加速效果明显，但是这种效果可能都是缓存作用的结果，而不是cdn加速的结果。我JS学得太差，暂时无从得知确切原因。

最后我测试了下实际效果，在chrome浏览器上至少第二次加载速度特别快，但是Firefox浏览器和Android端chrome浏览器都只能下载文件而无法实现在线阅读。

Firefox浏览器中不能在线浏览是IDM下载工具导致的，卸载IDM之后可以正常阅读。清理缓存后发现加速加载效果主要是靠缓存实现的，使用cndjs能加快加载速度但是不是瞬间开启。

用安装Ubuntu系统的电脑上的chrome浏览器实测发现页面颜色会发生变化，不知原因。引用新的cndjs后Android端chrome浏览器仍旧不能在线阅读，只能下载文件。此外可以用分页的方式加快访问速度，但我不会编辑相应代码，我还能接受现在这种阅读方式。这些问题留待以后解决！

## 创建pdf文档

[# 将JPG合并为PDF——将多个JPG图片合并为一个PDF文件，而不是多个PDF文件](https://cdkm.com/cn/merge-jpg-to-pdf)

简介：
1. 可添加最多100张图片，格式可以是JPG、PNG、GIF、WEBP或SVG等。
2. 拖放图片以对图片进行排序。点击图片并点击删除按钮可将其从列表中删除。
3. 设置选项，然后点击“开始合并”按钮。输出的PDF文件将会列在“输出文件”区域。|

下载生成的pdf文档时可以选择压缩pdf文档，因为在Github网页上上传文件大小上限是25MB。更大的文件需要用git-lfs从本地推送上去。


## 新建github仓库

我原本用hugo-embed-pdf来实现在线阅读，这是工具通过把pdf文件渲染成图片来阅读，但是在双分支结构下文件路径不好处理，打开页面总显示404让我内心崩溃。此外我希望打开一个新界面显示pdf文件必要时好可以下载到本地，而不是在那块小小区域来阅读pdf书籍。我于是在github上创建了个新仓库book。以下是在WSL2（Linux操作系统同理）上的操作：

```bash
mkdir book
cd book

mv   /mnt/e/pdfjs /home/RM/book

echo "# book" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Rosefinch-Midsummer/book.git
git push -u origin main
```

可能出现如下错误：
```
fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
错误显示本地仓库和远程仓库失去联系，因为提前执行了git remote add命令。按上面步骤即可正确推送。

## 和Github Pages仓库联结

开启github pages功能：

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230529133821.png)

[将你的文件上传到 GitHub](https://developer.mozilla.org/zh-CN/docs/Learn/Common_questions/Tools_and_setup/Using_GitHub_pages#%E5%B0%86%E4%BD%A0%E7%9A%84%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0%E5%88%B0_github)

1. 在当前页面上，你可能对本节的这部分感兴趣“**_…or push an existing repository from the command line_**（或者从命令行推送一个现有存储库）”。你应该看到本节中列出的两行代码。复制整个第一行，将其粘贴到命令行中，然后按 Enter 键。命令应该看起来像是这样的：
   
    BASHCopy to Clipboard
    
    ```
    git remote add origin https://github.com/chrisdavidmills/my-repository.git
    ```
    
2. 接下来，键入以下两个命令，每个命令之后按 Enter。这些指令将会把代码上传到 GitHub，并要求 Git 管理这些文件。
   
    BASHCopy to Clipboard
    
    ```
    git add --all
    git commit -m 'adding my files to my repository'
    ```
    
3. 最后，将代码推送到 GitHub，通过你正在访问的 GitHub 网页，然后输入我们看到的两个命令中的第二个命令“ **…or push an existing repository from the command line**（或从命令行部分推入现有存储库）部分”：
   
    BASHCopy to Clipboard
    
    ```
    git push -u origin master
    ```
    
4. 现在你需要为你的仓库开启 GitHub pages 分支。为此，其在仓库的主页中选择 _Settings_，然后从左侧的侧边栏中选择 _Pages_。在 _Source_ 下选择“main”分支。页面应该会自动刷新。
5. 重新回到 _GitHub Pages_ 部分，你应该会看到形式为“Your site is ready to be published at `https://xxxxxx`.”的一行内容。
6. 如果你点击这个 URL，你应该会跳转到你的示例的实时演示版本，提供的主页名为 `index.html`——这是默认的入口点。如果你的网站的入口点不是这个，例如 `myPage.html`，你需要访问 `https://xxxxxx/myPage.html`。



Suppose your personal website is hosted in a Github page as follows:

```
https://username.github.io
```

The repository should be name as **username.github.io**. If you have a pdf file named **document.pdf** and you place it in the directory **folder** then you should be able to open it directly in the browser through the following link:

```
https://username.github.io/folder/document.pdf
```

To allow the user to open the pdf in a new window in the browser, you may use the following HTML, where "PDF" points to the link:

```
<a href="https://username.github.io/folder/document.pdf" target="_blank">PDF.</a>
```

## 下载并上传相应的pdfjs文件夹

[# PDF.js——A general-purpose, web standards-based platform for parsing and rendering PDFs.](https://mozilla.github.io/pdf.js/)

我在建立仓库时就提前上传pdfjs文件夹了，这里不再介绍。如果之前没上传，可以从上面链接下载解压后手动上传。

## 调用cdnjs加速

cdnjs.cloudflare.com 是一个开放的免费 CDN（内容分发网络）服务，它提供了许多流行的前端库和框架，可以帮助开发人员更快速、高效地开发网站和应用程序。

### jspdf

[PDF Document creation from JavaScript](https://cdnjs.com/libraries/jspdf)

jspdf 是一个 JavaScript 库，用于在浏览器中生成 PDF 文件。

使用 cdnjs.cloudflare.com 上的 jspdf 库非常简单。只需在您的 HTML 页面中添加以下代码，就可以将该库包含到您的项目中：

`<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js" integrity="sha512-qZvrmS2ekKPF2mSznTQsxqPgnpkI4DNTlrdUmTzrDgektczlKNRRhy5X5AAOnx5S09ydFYWWNSfcEqDTTHgtNA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>`


### pdfjs

[下载地址](https://cdnjs.com/libraries/pdf.js)

在HTML页面直接调用下面的JS脚本即可。

URL：
```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf.min.js"></script>
```

Script Tag：
```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf.min.js" integrity="sha512-KEoL9wKXt/fhlAfN+ZNXf3pI48aaQE9Qd5fihHY+5n5XLTSnyGJ0uKgUj//V6KAcjFwzAbCYYPKeGlFES/H5Ng==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>

```
主要有下面几种压缩后（压缩能加快加载速度）的脚本，但我不知道它们具体有什么区别👀。
```txt
https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf.min.js

https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf.sandbox.min.js

https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf.worker.entry.min.js

https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf.worker.min.js

https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf_viewer.min.css

https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf_viewer.min.js
```
这将从 CDN 中获取 jspdf 库的最新版本并将其添加到所需项目中。

## 实测

简易语法

```javascript
<a href="https://rosefinch-midsummer.github.io/book/file/the-dictators-handbook-pdfepub-free.pdf" target="_blank">PDF文件在线阅读</a>

<script src=" https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.6.172/pdf.min.js"> </script>
```
文件名最好用英语而不是汉语，便于解析。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost01/img/20230529140110.png)











