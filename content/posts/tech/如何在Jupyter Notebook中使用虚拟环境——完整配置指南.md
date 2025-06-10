---
title: "如何在Jupyter Notebook中使用虚拟环境——完整配置指南"
date: 2025-06-10T18:34:25+08:00
lastmod: 2025-06-10T22:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- Python
- UV
- Jupyter Notebook
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


# 如何在Jupyter Notebook中使用虚拟环境——完整配置指南

Jupyter Notebook 是数据分析、交互式计算和可视化的强大工具。为了保持项目依赖的隔离和管理，很多开发者会使用虚拟环境（如`venv`、`conda`环境等）。本文结合实际操作经验和官方指导，详解如何在Jupyter Notebook中正确使用和管理虚拟环境，使得每个项目都能拥有独立的运行环境，避免包版本冲突。

## 1. 为什么要在Jupyter中使用虚拟环境

在数据科学或软件开发中，不同项目往往依赖不同版本的包。如果所有项目都用同一个全局Python环境，容易导致版本冲突和环境混乱。使用虚拟环境：

- 保证项目依赖一致性
- 防止全局环境被污染
- 方便切换和管理不同项目环境

但创建虚拟环境后，默认Jupyter Notebook无法直接识别这些环境，需要手动配置。

---

## 2. 利用`uv`工具管理虚拟环境下的Jupyter操作

`uv`是一个现代虚拟环境管理工具，它可以让你在项目的虚拟环境下运行Jupyter，并与项目环境无缝集成。

- **启动Jupyter服务器：**
    
    在项目目录，执行：
    
    ```bash
    uv run --with jupyter jupyter lab
    ```
    
    这样启动的Jupyter Lab服务器默认访问[http://localhost:8888/lab](http://localhost:8888/lab)，且所有引入的包都来自项目虚拟环境。
    
- **创建独立Kernel方便安装包：**
    
    若想在Notebook中安装新包，需要创建专门的kernel，步骤如下：
    
    1. 添加`ipykernel`为开发依赖：
        
        ```bash
        uv add --dev ipykernel
        ```
        
    2. 创建kernel，绑定到当前项目虚拟环境：
        
        ```bash
        uv run ipython kernel install --user --env VIRTUAL_ENV $(pwd)/.venv --name=project
        ```
        
        其中`--name=project`是kernel名称，可根据项目自行命名。
        
    3. 重新启动：
        
        ```bash
        uv run --with jupyter jupyter lab
        ```
        
    4. 新建Notebook时选择刚刚创建的`project` kernel。
        
    
    在Notebook中，可以使用命令如：
    
    ```bash
    !uv add pydantic
    ```
    
    将`pydantic`添加为项目依赖；或者
    
    ```bash
    !uv pip install pydantic
    ```
    
    在环境中临时安装包。这样`import pydantic`就可以直接使用。
    

---

## 3. 使用Anaconda虚拟环境在Jupyter中添加Kernel

如果你使用的是Anaconda管理虚拟环境，下面步骤可以使Jupyter识别这些环境：

- 进入命令行，激活目标环境，例如：
    
    ```bash
    activate tf1
    ```
    
- 检查该环境是否有`jupyter`和`ipykernel`包：
    
    ```bash
    conda list
    ```
    
- 如果缺少，使用conda安装：
    
    ```bash
    conda install jupyter
    conda install ipykernel
    ```
    
    如果conda安装过程慢或者失败，建议使用清华镜像源：
    
    ```bash
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple ipykernel
    ```
    
- 将环境添加到Jupyter Kernel列表：
    
    ```bash
    python -m ipykernel install --user --name tf1 --display-name "tf1"
    ```
    
    这里`--name`是内核名，`--display-name`是显示名。
    
- 验证安装是否成功：
    
    ```bash
    jupyter kernelspec list
    ```
    
    如果看到`tf1`，说明添加成功。
    
- 启动Jupyter Notebook后，即可在Kernel选择菜单中看到并使用`tf1`环境。
    
- **删除Kernel：**
    
    如果某内核不再需要，可以用以下命令删除：
    
    ```bash
    jupyter kernelspec remove tf1
    ```
    

---

## 4. 常见问题与解决方案

- **安装包失败或超时**  
    多数情况下是网络问题，推荐切换Python包源为国内高速镜像（如清华源）。
    
- **Kernel添加后Jupyter无显示**  
    检查环境激活是否正确，确保当前环境中有`ipykernel`和`jupyter`。
    
- **虚拟环境和Notebook不匹配**  
    通过`jupyter kernelspec list`确认kernel目录，并检查对应的python路径是否正确。
    

---

## 5. 小结

通过本文介绍的方法，无论是使用`uv`工具管理的虚拟环境，还是Anaconda创建的环境，都可以方便地集成到Jupyter Notebook中，实现项目依赖的独立管理和灵活扩展。虚拟环境的正确使用，不仅能让你的代码更稳定，也让协作和部署更加简单高效。

改进版 Windows11 批处理脚本：

```bat
@echo off
cd /d D:\AI
uv run --with jupyter jupyter notebook .
```

---

**版权声明**：本文参考并整合自[uv官方文档](https://docs.astral.sh/uv/guides/integration/jupyter/)及CSDN博客作者文章，遵循CC4.0 BY-SA协议。转载请注明出处。














