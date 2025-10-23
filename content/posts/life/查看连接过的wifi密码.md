---
title: "查看连接过的wifi密码"
date: 2023-05-20T20:35:25+08:00
lastmod: 2025-09-22T21:54:22+08:00
categories:
- 计算机网络
- 网络安全
tags:
- wifi
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




## Windows10 下查看连接过的wifi密码

win+R弹出框内输入cmd

 ![r](https://img2020.cnblogs.com/blog/1020884/202012/1020884-20201212151436062-1870549067.png)

 

然后命令行内输入`netsh wlan show profiles` 回车，把周围的所有WiFi名称都显示出来

 ![r](https://img2020.cnblogs.com/blog/1020884/202012/1020884-20201212235411393-1117446773.png)

最后再重新输入上面的代码后面加多“WiFi名字” key=clear 回车即可；关键内容就是WiFi的密码了

如：`netsh wlan show profiles "408专属光纤" key=clear`

 

 ![r](https://img2020.cnblogs.com/blog/1020884/202012/1020884-20201212235552693-409557473.png)


## Ubuntu下查看连接过的wifi密码


```shell
cd /etc/NetworkManager/system-connections && ls  #查看连接过的wifi名称

sudo cat 'MERCURY_404'  #打印选定的wifi信息
```

输出内容：
```bash
[connection]
id=MERCURY_404
uuid=4a9c908a-1c00-492c-bb16-2794rea450d4
type=wifi
permissions=

[wifi]
mac-address=E4:70:C8:85:A0:DF
mac-address-blacklist=
mode=infrastructure
ssid=MERCURY_404

[wifi-security]
auth-alg=open
key-mgmt=wpa-psk
psk=XXXxx #密码

[ipv4]
dns-search=
method=auto

[ipv6]
addr-gen-mode=stable-privacy
dns-search=
method=auto

```





