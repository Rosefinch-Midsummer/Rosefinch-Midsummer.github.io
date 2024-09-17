---
title: "（转载）部署React-Vite Application"
date: 2024-09-17T18:34:25+08:00
lastmod: 2024-09-17T22:54:22+08:00
draft: false
math: true
categories:
- 编程
tags:
- 静态网站部署
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

# Deploying a React Vite Application on Render

## 前言

[原文链接](https://medium.com/technogise/deploying-a-react-vite-application-on-render-8eb9caeaa502)

作者：Tushar Mahajan

发布时间：Apr 10, 2024

When it comes to deployment, Render.com provides a user-friendly platform that integrates seamlessly with your Git workflow. This article will guide you through the process of deploying your React Vite application to Render.com, ensuring a smooth and efficient transition from development to production.

![](https://miro.medium.com/v2/resize:fit:1050/1*PbhS1UYtKUQKcXEGbZM40w.png)

## **Prerequisites:**

- A React application created using Vite
- A Render.com account. If you haven’t signed up yet, head over to [Render’s website](https://render.com/) to create an account. (Free tier available)
- A GitHub or GitLab account is required to connect your repository with Render.com.

## Deploying on Render

I plan to use a basic React Vite application to demonstrate deploying on Render, which is available on my GitHub Account — [NoteKeeper](https://github.com/mahajant99/NoteKeeper).

First, let’s create a new Static Site on Render.

![](https://miro.medium.com/v2/resize:fit:1050/1*jCCxwU85uzkfUHb2IUoLxw.png)

Go to the Render.com dashboard, click the “New” button, and select “Static Site”

![](https://miro.medium.com/v2/resize:fit:1050/1*9OziMqsEPIAULwKkn1-fmA.png)

Select the Git provider that hosts your React Vite app’s repository or you can enter link for any public repository. In my case I am going to connect my Static Site with NoteKeeper repository.

![](https://miro.medium.com/v2/resize:fit:1050/1*pO3gWaLdM4EHbxZC8Gw3bg.png)

Specify the project name, branch, etc as needed.

- In the "Build Commands" section, enter the following commands:

npm install; npm run build

- In the “Publish Directory” section, specify the directory containing your built application’s static assets. For React Vite Application set the Root Directory as _dist._

dist

- Customize additional settings as needed (environment variables, Auto-Deploy, etc.).
- Once you’re satisfied with the configuration, click “Create Static Site” to initiate the deployment process.

![](https://miro.medium.com/v2/resize:fit:1050/1*rgANHHI0bvn3xzc1hs_lMA.png)

- Render will automatically build and deploy your React Vite application based on the provided commands and directory.

![](https://miro.medium.com/v2/resize:fit:1050/1*MCeWeBJHYGhYNJXNIVlkCA.png)

- Upon successful deployment, your application will be marked as Live, and a unique URL will be provided for you to access it.
- You can view your live React Vite application by navigating to the generated URL in your web browser.

My application is available at [https://notekeeper-851u.onrender.com/](https://notekeeper-851u.onrender.com/).

## Conclusion

Deploying a React Vite application on Render.com is a straightforward process that streamlines the transition from development to production. By following these steps, you’ll have your React Vite application up and running on Render.com in no time. Happy Deployment!



# Vite-React-APP Deploy on GitHub

## 自定义模板

[vite-react-deploy](https://github.com/Rosefinch-Midsummer/vite-react-deploy)


## Deploy Vite React App to GitHub Pages

[原文链接](https://www.vd-developer.online/blog/vite-react-deploy-github)

发布时间：Apr 26, 2024

## Fixing Empty Pages & Missing Assets in Vite React + React Router (GitHub Pages)

[原文链接](https://www.vd-developer.online/blog/fix-vite-react-empty-pages-missing-assets)

发布时间：Jun 9, 2024


# 静态网站和动态网站

静态网站和动态网站的区别在于网站的内容是如何管理和呈现的。

静态网站是指网站的内容在服务器上提前生成好并保存为静态文件，用户在访问网站时直接获取这些静态文件进行展示。静态网站的内容一般不会改变，除非手动修改文件内容。

动态网站是指网站的内容是在用户访问时通过服务器端程序动态生成的，内容可以根据用户的请求或其他条件实时改变。动态网站通常使用数据库和服务器端脚本语言来实现内容的动态生成和管理。

根据描述，添加了Emailjs交互功能和three.js 3d模型但没有数据库交互的网站可以被认定为静态网站，因为内容是提前生成好的静态文件，并不需要服务器端动态生成。









