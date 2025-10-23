---
title: "Python虚拟环境管理工具UV和JupyterNotebook联动"
date: 2025-05-23T12:34:25+08:00
lastmod: 2025-05-23T12:54:22+08:00
math: true
categories:
- 计算机
- 编程
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

# Python虚拟环境管理新利器——uv全解析

Python项目开发中，虚拟环境和依赖管理一直是让人头疼的话题。今天给大家介绍一个极致高速、功能强大的Python包和项目管理工具——**uv**，它由Rust语言编写，是由著名的[Astral](https://astral.sh/)团队打造，同时也是性能爆棚的[代码检查工具Ruff](https://github.com/astral-sh/ruff)的作者开发。

---

## 一、什么是uv？

uv是一款极其快速的Python包和项目管理工具，支持项目依赖管理、虚拟环境创建、脚本执行、命令行工具管理和Python版本切换。uv试图集成`pip`、`virtualenv`、`pipx`等工具的能力，并通过Rust优化性能，带来10~100倍的速度提升。

---

## 二、安装uv

### 1. 脚本安装（macOS/Linux）

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### 2. PowerShell安装（Windows）

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### 3. PyPI安装

```bash
pip install uv
```

或者使用pipx安装：

```bash
pipx install uv
```

安装后可使用内置命令自我升级：

```bash
uv self update
```

更多安装详情和方法请参考官方文档：[安装文档](https://docs.astral.sh/uv/getting-started/installation/)。

---

## 三、核心功能介绍

### 1. 项目管理

uv提供类似`poetry`或`rye`的项目管理能力：

- 快速初始化项目：`uv init example`
- 快速添加依赖并自动创建虚拟环境：`uv add ruff`
- 运行项目命令：`uv run ruff check`
- 锁定依赖版本：`uv lock`
- 同步依赖：`uv sync`

示例：

```bash
$ uv init example
$ cd example
$ uv add ruff
$ uv run ruff check
$ uv lock
$ uv sync
```

详细项目使用指南见[官方项目文档](https://docs.astral.sh/uv/guides/projects/)。

### 2. 脚本依赖管理

可以为单个.py脚本声明依赖，并在隔离环境中执行：

```bash
echo 'import requests; print(requests.get("https://astral.sh"))' > example.py
uv add --script example.py requests
uv run example.py
```

这让快速编写带依赖的小工具变得十分便捷。[脚本使用指南](https://docs.astral.sh/uv/guides/scripts/)。

### 3. 命令行工具管理

通过`uvx`快速在临时环境运行CLI工具，也可永久安装：

```bash
uvx pycowsay 'hello world!'

uv tool install ruff
ruff --version
```

类似`pipx`，方便管理Python工具链。[工具管理文档](https://docs.astral.sh/uv/guides/tools/)。

### 4. Python版本管理

uv内置Python版本管理功能，支持多版本安装与切换：

```bash
uv python install 3.10 3.11 3.12

uv venv --python 3.12.0

uv run --python pypy@3.8 -- python --version

uv python pin 3.11
```

官方文档：[Python版本安装指南](https://docs.astral.sh/uv/guides/install-python/)。

### 5. pip接口增强

uv提供对`pip`，`pip-tools`和`virtualenv`的替代接口，兼容现有工作流，且性能提升显著：

- 精确锁定依赖版本
- 跨平台的依赖文件生成
- 虚拟环境简单创建与依赖同步

示例：

```bash
uv pip compile docs/requirements.in --universal --output-file docs/requirements.txt

uv venv

uv pip sync docs/requirements.txt
```

详细请见：[pip接口文档](https://docs.astral.sh/uv/pip/index/)。

---

## 四、总结

uv是一款集包管理、虚拟环境、Python版本管理、脚本依赖及CLI工具管理于一体的现代化Python管理工具。依靠Rust的高速执行内核，极大提升了开发体验和效率，非常适合追求极速与高效的Python开发者。

如果你还在用传统pip+virtualenv，或者想体验更智能的Python多版本管理和项目隔离，不妨试试uv，相信它会成为你新的生产力工具。

---

### 相关文章与资源

- 官方主页：[https://astral.sh/uv](https://astral.sh/uv)
- GitHub仓库：[https://github.com/astral-sh/uv](https://github.com/astral-sh/uv)
- 官方文档：[https://docs.astral.sh/uv](https://docs.astral.sh/uv)


# 使用 uv 与 Jupyter 集成指南

[Jupyter](https://jupyter.org/) 作为交互式计算、数据分析和可视化的利器，深受开发者欢迎。利用uv，你可以灵活地将Jupyter集成到项目环境中，或作为独立工具使用。

---

## 1. 在项目中使用 Jupyter

如果你正在使用uv管理项目依赖和虚拟环境，可以通过以下命令启动访问项目虚拟环境的Jupyter服务器：

```bash
uv run --with jupyter jupyter lab
```

默认情况下，`jupyter lab` 会在 [http://localhost:8888/lab](http://localhost:8888/lab) 启动服务。

在Notebook中，你可以像平时一样导入项目依赖的库（如`requests`），这些库都来源于项目专属的虚拟环境。

### 1.1 创建专用Kernel（内核）

如果计划在Notebook里直接安装新的依赖，建议为项目创建一个独立Kernel。这样Jupyter服务和Notebook分别运行在不同环境，安装依赖时可以确保作用于项目环境。

步骤如下：

- 以开发依赖安装`ipykernel`：

```bash
uv add --dev ipykernel
```

- 为项目创建Kernel：

```bash
uv run ipython kernel install --user --env VIRTUAL_ENV=$(pwd)/.venv --name=project
```

- 重启Jupyter服务：

```bash
uv run --with jupyter jupyter lab
```

打开Notebook时，在内核选择器中选`project`内核。此时，可以用：

```bash
!uv add pydantic
```

往项目依赖中添加`pydantic`，或者用

```bash
!uv pip install pydantic
```

仅在虚拟环境安装`pydantic`，但不更新项目配置文件（如`pyproject.toml`、`uv.lock`）。两种方式均可在Notebook内直接使用`import pydantic`。

### 1.2 不创建Kernel时安装包

若不想创建Kernel，也可在Notebook里安装包。但需注意：

- 以`uv run --with jupyter`启动时，Notebook中执行`!uv add`会修改项目的虚拟环境，`import`立即生效。
- 执行`!uv pip install`则只会影响Jupyter服务器所处的环境（非项目环境），且该依赖只在当前Jupyter会话有效，重启服务后失效。
- 如果需要在Notebook中使用`%pip`魔法命令，建议先用：

```bash
uv venv --seed
uv run --with jupyter jupyter lab
```

这样Notebook里通过`%pip install`安装的软件包会添加到项目的虚拟环境中，但不会同步更新项目依赖配置。

---

## 2. 独立模式下使用 Jupyter

想临时运行Jupyter进行快速测试，可用：

```bash
uv tool run jupyter lab
```

此命令启动一个独立、隔离的Jupyter环境，不依赖任何项目。

---

## 3. 在非项目环境中使用 Jupyter

若你有一个没有`pyproject.toml`或`uv.lock`的虚拟环境，也能安装Jupyter并使用：

```bash
uv venv --seed
uv pip install pydantic
uv pip install jupyterlab
.venv/bin/jupyter lab
```

此时Notebook内可`import pydantic`，也能通过`!uv pip install`或`!pip install`安装其他包。

---

## 4. 在 VS Code 中使用 uv 管理的 Jupyter

VS Code 支持Jupyter Notebook，推荐在uv项目中为Notebook创建Kernel，步骤如下：

```bash
uv init project
cd project
uv add --dev ipykernel
code .
```

- 在VS Code中打开项目目录
- 通过命令面板选择“创建Jupyter Notebook”，启动时选择“Python Environments”下的项目虚拟环境（macOS/Linux为`.venv/bin/python`，Windows为`.venv\Scripts\python`）

> **注意**  
> VS Code要求`ipykernel`必须安装在项目环境中。若不想作为开发依赖安装，也可以直接用`uv pip install ipykernel`安装。

如果想在Notebook中用`!uv add`或`!uv pip install`操作项目环境，建议先将`uv`本身也加为开发依赖：

```bash
uv add --dev uv
```

这样能更方便地管理Notebook中的依赖安装和同步。

---

# 小结

利用uv对Jupyter的支持，可以轻松实现：

- 在项目中启动Jupyter，自动隔离环境
- 创建专用Kernel保证依赖安装归属清晰
- 在无Kernel情况下灵活安装包
- 独立启动Jupyter实验环境
- 在VS Code等编辑器流畅使用uv管理的项目环境


# Juvio：支持依赖管理、可复现且友好的Git集成Jupyter笔记本

[Juvio](https://github.com/OKUA1/juvio) 是一个帮助你在Jupyter笔记本中实现**可复现依赖管理**和**简洁版本控制**的工具，专为Python数据科学和交互式编程设计。

---

## 主要功能

### 💡 内嵌依赖管理

你可以直接在笔记本中安装所需包：

```python
%juvio install numpy pandas
```

这些依赖会以[PEP 723](https://peps.python.org/pep-0723/)规范的形式，自动保存为笔记本中的元数据：

```python
# /// script
# requires-python = "==3.10.17"
# dependencies = [
#   "numpy==2.2.5",
#   "pandas==2.2.3"
# ]
# ///
```

这样，笔记本自身就记录了完整的运行环境需求。

### ⚙️ 自动环境搭建

每次打开笔记本时，Juvio会自动通过**uv**创建临时虚拟环境并安装相应依赖，保证代码在正确的Python和包版本下运行，真正实现环境复现。

### 📁 Git 友好格式

Juvio自动将笔记本转换成基于`# %%`分块的脚本格式，方便Git进行差异对比，解决了传统`.ipynb`文件难以直观比对的问题：

```python
# %%
%juvio install numpy
# %%
import numpy as np
# %%
arr = np.array([1, 2, 3])
print(arr)
# %%
```

---

## 如何使用 Juvio

> ⚠️ 目前 Juvio 处于**测试阶段**，可能存在一些不稳定或缺陷，欢迎[提issue反馈](https://github.com/OKUA1/juvio/issues)。

1. 安装Juvio：

```bash
pip install juvio
jupyter labextension enable juvio-frontend
```

2. 确保你已安装了`uv`（安装文档见：[https://docs.astral.sh/uv/getting-started/installation/）](https://docs.astral.sh/uv/getting-started/installation/%EF%BC%89)
    
3. 启动JupyterLab，创建并打开一个Juvio支持的笔记本。
    
4. 在笔记本中用`%juvio install ...`安装依赖，运行代码。
    

> **已知问题：** 如果遇到“Notebook does not appear to be JSON”的错误，尝试用以下命令启动JupyterLab：

```bash
jupyter lab --ServerApp.jpserver_extensions="{'juvio': True}"
```

这样可以避免启动时的兼容性问题。

---

## 为什么选择 Juvio？

- 不需要额外的`lock`或`requirements`文件，依赖直接内嵌记录
- 环境可复现，确保代码随时可重现运行
- 生成更干净、易读的Git diff，极大方便版本管理

---

## 技术支持

- 由高速Python包管理工具`uv`驱动环境管理
- 遵循标准的Python内嵌依赖格式（PEP 723）
- 采用类似`jupytext`的脚本分块格式，方便版本控制

---

Juvio让Jupyter笔记本更易管理和共享，提升科研与开发工作流的可维护性和效率。如果你关心笔记本的依赖管理和代码复现，强烈推荐试用！









