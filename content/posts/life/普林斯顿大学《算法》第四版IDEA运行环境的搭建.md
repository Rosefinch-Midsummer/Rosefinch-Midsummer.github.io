---
title: "普林斯顿大学《算法》第四版 IDEA 运行环境的搭建"
date: 2024-02-26T19:34:25+08:00
lastmod: 2024-02-26T22:54:22+08:00
math: true
categories:
- 在线课程
- 计算机
tags:
- Coursera
- 算法
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



# 普林斯顿大学《算法》第四版 IDEA 运行环境的搭建

[《算法》第四版 IDEA 运行环境的搭建](https://www.cnblogs.com/junhong1995/p/7769006.html)

环境的搭建分以下几个步骤:

- Java 运行环境的搭建
- IDEA 的安装与破解
- 《算法》 运行库的下载与配置
- IDEA 工程的创建以及在IDEA中使用命令行

前两个步骤就不写了，网上的教程一大把。

## **《算法》 运行库的下载与配置**

1.首先，我们需要下载作者提供的运行库，下载地址： [点我下载](http://algs4.cs.princeton.edu/code/) ，

![下载红色框框的内容](https://images2017.cnblogs.com/blog/785907/201711/785907-20171101225612841-1001244476.png "下载红色框框的内容")

  

下载红色框框的内容

我们需要下载两个内容，一个是库，一个是测试的数据。库是algs4.jar，数据是algs4-data.zip。

2.在C盘建立目录 _C:\Program Files\algs4_ 将 algs4.jar 放入其中，如下所示：

![algs4.jar的存放位置](https://images2017.cnblogs.com/blog/785907/201711/785907-20171101225613138-1141007736.png "algs4.jar的存放位置")

  

algs4.jar的存放位置

ps：这里你可以放在任何你想要放的地方，笔者只是习惯放在C盘而已。

3.在CLASSPATH环境变量中，添加值 `C:\Program Files\algs4\algs4.jar` (就是刚刚存放algs4.jar的路径)，如下所示：

![环境变量的设置](https://images2017.cnblogs.com/blog/785907/201711/785907-20171101225613373-1893075059.png "环境变量的设置")

环境变量的设置

网上说，要加个 分号 ，具体我也没去深究，就这样吧。

这样下来，就完成了库的配置了。还有一个测试数据的使用，在下一节。

## **IDEA 工程的创建以及在IDEA中使用命令**

1.创建一个HelloWorld工程

![enter description here](https://images2017.cnblogs.com/blog/785907/201711/785907-20171101225613638-847285273.png "enter description here")

选择你的JDK，我使用的是1.6。

2.为项目添加jar包

配置`IDEA`,打开`File--->Project Structure`

![Project Structure](https://images2017.cnblogs.com/blog/785907/201711/785907-20171101225614060-1546215492.png "Project Structure")


![添加jar包](https://images2017.cnblogs.com/blog/785907/201711/785907-20171101225614513-646694477.png "添加jar包")

添加jar包

3.解压测试数据到src目录下：

![解压测试数据到src目录下](https://images2017.cnblogs.com/blog/785907/201711/785907-20171101225614857-1937471381.png "解压测试数据到src目录下")

解压测试数据到src目录下

## IDEA中重定向配置

《算法》中的代码很多都需要使用terminal进行命令行执行，而且重定向符号“<"经常被用到，例如开头这段二分查找算法的命令：

![e](https://img-blog.csdnimg.cn/8c5fd1f80b4148a9b6710080ea24bd5c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATWFqb3JUb20zMw==,size_13,color_FFFFFF,t_70,g_se,x_16)

但是在IDEA中通过terminal执行这行命令的时候会得到如下错误（“<”运算符是为将来使用而保留的。）：

![a](https://img-blog.csdnimg.cn/803d4a4cfe21479095a6b5bdfcbfa80a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATWFqb3JUb20zMw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这时候我们需要在IDEA中对重定向进行配置（Run > Configrations）：

![a](https://img-blog.csdnimg.cn/97e9825c7bd844f187431d756730eb0d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATWFqb3JUb20zMw==,size_20,color_FFFFFF,t_70,g_se,x_16)

这样我们就可以得到测试结果了：

![a](https://img-blog.csdnimg.cn/d8675bb19e4c47a782e6f7c9e584b9b2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBATWFqb3JUb20zMw==,size_20,color_FFFFFF,t_70,g_se,x_16)

## Coursera普林斯顿算法作业一

[知乎专栏文章](https://zhuanlan.zhihu.com/p/545276738)

### HELLO,WORLD

本次作业是可选的。它主要目标是确保你可以书写简单的 Java 程序，使用 _algs4.jar_，并且提交它们到 _Coursera autograder_。

0. 创建我们的 Java 编程环境(可选)。通过指导书一步一步在你们的计算机上，创建新手友好的 Java 编程环境。在每次作业，从顶部的菜单中使用 Project。

作为指导的一部分，你将书写，编译，并且执行 HelloWorld.java 程序。

```text
~/Desktop/hello> javac HelloWorld.java

~/Desktop/hello> java HelloWorld
Hello, World
```

1. 命令行参数。程序 HelloGoodbye.java 接受两个命令行参数，并且输出 hello 和 goodbye 消息，如下所示（hello 消息的名字按顺序，goodbye 消息的名字逆序）。

```text
~/Desktop/hello> javac HelloGoodbye.java

~/Desktop/hello> java HelloGoodbye Kevin Bob
Hello Kevin and Bob.
Goodbye Bob and Kevin.

~/Desktop/hello> java HelloGoodbye Alejandra Bahati
Hello Alejandra and Bahati.
Goodbye Bahati and Alejandra.
```

2. 使用 algs4.jar。正在完善。编写 RandomWord.java 程序，从标准输入中读取一串单词，并且随机输出这些单词中的一个。不要存储这些单词在数组或者链表中，使用 Knuth 的方法：当读到第 i 个单词，以概率 1/i 选择它作为冠军，来代替之前的冠军。在读取所有单词之后，输出最后的冠军。

```text
~/Desktop/hello> javac-algs4 RandomWord.java

~/Desktop/hello> java-algs4 RandomWord
heads tails
tails

~/Desktop/hello> java-algs4 RandomWord
heads tails
heads

~/Desktop/hello> more animals8.txt
ant bear cat dog
emu fox goat horse

~/Desktop/hello> java-algs4 RandomWord < animals8.txt
emu

~/Desktop/hello> java-algs4 RandomWord < animals8.txt
bear
```

使用如下来自 algs4.jar 的库函数

- StdIn.readString()：从标准输入中读取并返回下一个字符串。
- StdIn.isEmpty()：如果标准输入中不再有可用的字符串，返回 true。否则，返回 false。
- StdOut.println()：向标准输出打印字符串和换行符。可以使用 System.out.println() 代替。
- StdRandom.bernoulli(p)：概率 p 的情况返回 true，概率 1 - p 的情况返回 false。

为了访问这些库函数，你必须做如下两件事：

- 添加 algs4.jar 到 java classpath。

如果使用 IntelliJ，需要项目目录包含 algs4.jar 并且添加到 java classpath。

- 在程序最上方添加 import 语句

```java
import edu.princeton.cs.algs4.StdIn;
import edu.princeton.cs.algs4.StdOut;
import edu.princeton.cs.algs4.StdRandom;
```

网站提交。提交的 ZIP 文件只包含 HelloWorld.java，HelloGoodbye.java 和 RandomWorld.java。除了上面列举的 java.lang 和 algs4.jar 之外，不允许调用其它库。

### 解答

### ex1

直接输出 hello,world

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
```

### ex2

很粗暴，默认输入两个值，不能用循环，很僵硬

```java
public class HelloGoodbye {
    public static void main(String[] args) {
        System.out.print("Hello");
        System.out.print(" " + args[0] + " and");
        System.out.println(" " + args[1] + ".");

        System.out.print("Goodbye");
        System.out.print(" " + args[1] + " and");
        System.out.println(" " + args[0] + ".");
    }
}
```

### ex3

按照题目要求完成，没有什么需要动脑的地方

```java
import edu.princeton.cs.algs4.StdIn;
import edu.princeton.cs.algs4.StdOut;
import edu.princeton.cs.algs4.StdRandom;

public class RandomWord {

    public static void main(String[] args) {
        String res = "";
        String tmp = "";
        double p = 1.0;

        while (!StdIn.isEmpty()) {
            tmp = StdIn.readString();
            if (StdRandom.bernoulli(1 / p)) {
                res = tmp;
            }
            p++;
        }

        StdOut.println(res);
    }
}
```

![](https://pic3.zhimg.com/80/v2-75f9b76bf83306c77204171a506a88c6_1440w.webp)

发布于 2022-07-23 16:07

## 附录：没有重启IDEA时代码可能报错IntelliJ IDEA Cannot resolve method println(java.lang.String)

重启或是执行下面操作：

File -> Invalidate Caches / Restart…  

清空缓存就可以了









