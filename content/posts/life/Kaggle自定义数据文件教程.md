---
title: "Kaggle自定义数据文件教程"
date: 2025-04-28T12:34:25+08:00
lastmod: 2026-01-01T11:54:22+08:00
math: true
categories:
- 编程
- 计算机
tags:
- Kaggle
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

### 什么是Kaggle？

Kaggle是全球领先的数据科学竞赛平台，提供丰富的数据集和强大的在线笔记本环境，让用户能够在云端进行数据分析、模型训练和分享。Kaggle不仅支持公开数据集，也允许用户上传自定义数据，方便进行个性化实验。

### PyTorch简介

PyTorch是当前非常流行的深度学习框架之一，特别适合研究和快速原型开发。它提供了灵活的动态图机制，并拥有丰富的工具和库支持，如自动求导、神经网络模块和数据加载工具。

### torchvision.datasets详解

`torchvision.datasets`是PyTorch生态中非常实用的模块，内置了多个常见视觉数据集的加载接口（如MNIST、CIFAR10、FashionMNIST等）。其主要功能包括：

- 自动下载数据
- 读取数据文件和标签
- 支持预处理和变换（transforms）
- 方便的训练/测试数据区分

使用时，有几个关键参数需要留意：

- `root`：数据集根目录，存放数据的地方
- `train`：是否加载训练集（True）或测试集（False）
- `download`：数据不存在时是否自动下载
- `transform`：对加载的图像进行预处理，如转Tensor、归一化
- `target_transform`：对标签的处理

在Kaggle这种环境下，常用的做法是先将数据上传到`/kaggle/input`目录，然后复制到工作目录，再通过`datasets`模块的接口加载。

### shutil模块简介

`shutil`是Python的高级文件操作模块，常用来进行文件和文件夹的复制、移动、删除等操作，较`os`模块更简洁且功能集中。在处理数据搬运时非常方便，例如：

- `shutil.copytree()`：递归复制文件夹及内容
- `shutil.rmtree()`：递归删除文件夹及所有内容

---

## 具体流程

### 1. 上传数据集

将数据集文件夹通过Kaggle界面上传，假设命名为`mnist-data`。上传后文件会出现在路径`/kaggle/input/mnist-data`下。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost05/img20250429121936.png)

### 2. 创建目录并迁移数据

有两种常见方式将数据从输入目录复制到工作目录：

#### 方式1：使用`os`结合Linux命令`cp`

```python
import os 

output_path = "/kaggle/working/data/MNIST/raw"

# 创建输出目录（递归创建，避免路径不存在报错）
os.makedirs(output_path, exist_ok=True)

# 使用Linux命令复制文件
!cp -r /kaggle/input/mnist-data/* /kaggle/working/data/MNIST/raw
```

#### 方式2：Python内置模块`shutil.copytree()`

```python
import shutil

input_path = "/kaggle/input/mnist-data"
output_path = "/kaggle/working/data/MNIST"

# 复制整个文件夹及其内容（copytree会自动创建目标路径）
shutil.copytree(input_path, output_path)
```

🔔注意事项：

- `shutil.copytree()`不能复制到已存在的目录，会报错。如果目录存在，建议先删除或用`shutil.copytree(..., dirs_exist_ok=True)`(Python 3.8+支持)。
- `os.makedirs()`确保目标文件夹存在。

---

### 3.迁移后数据目录展示


![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost05/img20250429122412.png)

### 4. PyTorch导入数据并输出数据维度

通过`torchvision.datasets`加载数据：

```python
from torchvision import datasets
from torchvision.transforms import ToTensor

train_data = datasets.MNIST(
    root="./data",         # 指定数据存放根目录
    train=True,            # 加载训练集
    download=False,        # 数据已上传，本地已有就不用自动下载
    transform=ToTensor(),  # 转换为Tensor方便PyTorch使用
    target_transform=None
)

test_data = datasets.MNIST(
    root="./data",
    train=False,
    download=False,
    transform=ToTensor(),
    target_transform=None
)

print(f"训练集样本数量: {len(train_data)}")
print(f"测试集样本数量: {len(test_data)}")
```

这里`datasets.MNIST`实际上会在`root`指定路径下尝试读取`MNIST`文件夹，并在其中查找数据文件（尤其是`raw`文件夹）。如果数据已上传并按照规范摆放，即可正常加载。

---


## 其余相关命令

### 获取默认工作目录

```python
import os
print(os.getcwd())
```

一般返回：

```
/kaggle/working
```

---

### 更改当前工作目录

```python
import os

input_path = "/kaggle/input"
os.chdir(input_path)
print(os.getcwd())  # 验证目录变更
```

---

### 创建目录

```python
import os

output_path = "/kaggle/working/data/MNIST/raw"
os.makedirs(output_path, exist_ok=True)
```

---

### 使用`shutil`删除目录

```python
import shutil

directory_path = "/kaggle/working/data/MNIST/"
shutil.rmtree(directory_path)  # 小心使用，删除目录及所有内容
```

---

### 使用`shutil`复制文件夹

```python
import shutil

input_path = "/kaggle/input/mnist-data"
output_path = "/kaggle/working/data/MNIST"
shutil.copytree(input_path, output_path, dirs_exist_ok=True)  # Python 3.8+支持覆盖复制
```

---

### 使用Linux命令`cp`复制文件

```python
!cp -r /kaggle/input/mnist-data/* /kaggle/working/data/MNIST/raw
```

---

## 总结

- 先上传数据集到`/kaggle/input`目录；
- 使用Python文件操作、`shutil`或Linux命令将数据复制到`/kaggle/working`工作目录；
- 使用`torchvision.datasets`加载数据，设置`root`路径及`transform`，加载自己上传的数据；
- 注意`shutil.copytree()`的新参数`dirs_exist_ok`可以避免已有目录错误；
- PyTorch的数据加载不仅限于MNIST，熟悉`datasets`使用可以方便加载多种常用视觉数据集。














