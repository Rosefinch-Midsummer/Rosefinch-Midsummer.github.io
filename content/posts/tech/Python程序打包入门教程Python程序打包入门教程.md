---
title: "Python程序打包入门教程"
date: 2025-02-10T10:34:25+08:00
lastmod: 2025-02-10T12:54:22+08:00
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


# Python程序打包入门教程

## 使用PyInstaller将代码打包成.exe文件

### 只打包一个Python文件

要将你的 Python 代码打包成一个可以直接执行的 `.exe` 文件，可以使用 `PyInstaller` 工具。以下是详细的步骤：

### 步骤 1: 安装 PyInstaller

首先，确保你的系统上安装了 `PyInstaller`。可以使用以下命令通过 `pip` 安装：

```bash
pip install pyinstaller
```

### 步骤 2: 打包你的代码

1. **保存你的代码**：将你的代码保存为一个 `.py` 文件，例如 `bilibili_downloader.py`。

2. **打开命令提示符**：在 Windows 中，打开命令提示符（CMD）。

3. **导航到代码所在的目录**：使用 `cd` 命令导航到你保存 Python 文件的目录。例如：

   ```bash
   cd C:\path\to\your\script
   ```

4. **使用 PyInstaller 打包**：运行以下命令来创建可执行文件：

   ```bash
   pyinstaller --onefile --windowed bilibili_downloader.py
   ```

   - `--onefile` 参数表示将所有内容打包成一个单独的 `.exe` 文件。
   - `--windowed` 参数用于创建不显示命令行窗口的 GUI 应用程序（适用于 wxPython 应用）。

### 步骤 3: 查找生成的 .exe 文件

打包完成后，`PyInstaller` 会在当前目录下创建一个 `dist` 文件夹，里面会包含你的可执行文件 `bilibili_downloader.exe`。

### 步骤 4: 运行 .exe 文件

你可以直接双击 `bilibili_downloader.exe` 文件来运行你的应用。

### 额外注意事项

- **依赖文件**：如果你的程序依赖于其他文件（例如图像、配置文件等），你可能需要将这些文件手动复制到 `dist` 文件夹中，或者在打包时使用 `--add-data` 参数指定它们。

- **测试**：在不同的电脑上测试生成的 `.exe` 文件，以确保它在没有 Python 环境的情况下也能正常运行。

- **防火墙和杀毒软件**：某些杀毒软件可能会误报新生成的 `.exe` 文件为恶意软件。在这种情况下，你可能需要将其添加到白名单中。

按照这些步骤，你应该能够成功将你的 Python 脚本打包成一个可执行的 `.exe` 文件。

---

## 打包多个Python文件

[pyinstaller打包python程序（多文件）](https://www.cnblogs.com/ronyjay/p/12713078.html)

在某些项目中，可能需要打包多个 Python 文件及其资源。以下是两种常用的方法：

### 方法 1: 使用命令行

可以使用命令行将多个文件打包：

```bash
pyinstaller [主文件] -p [其他文件1] -p [其他文件2] --hidden-import [自建模块1] --hidden-import [自建模块2]

# 例如：
pyinstaller -F start_menu.py -p check_default_speedup.py -p check_server_os.py -p check_speedup.py
```

### 方法 2: 使用spec文件

如果文件较多，使用spec文件会更加方便。

#### 2.1 创建spec文件

打开终端并进入项目路径下，输入指令：

```bash
pyinstaller -F start_menu.py
```

运行结束后，会在当前目录下生成 `start_menu.spec` 文件。删除生成的 `build` 和 `dist` 文件夹，只保留 `start_menu.spec` 文件。

#### 2.2 编辑spec文件

根据自己的项目需求编辑 `start_menu.spec` 文件：

```python
# -*- mode: python ; coding: utf-8 -*-

block_cipher = None

a = Analysis(['start_menu.py', 'check_default_speedup.py', 'check_server_os.py', 'check_speedup.py'],
             pathex=['D:\\Project\\python\\xxxTool'],
             binaries=[],
             datas=[],  # 此列表存放所有的资源文件
             hiddenimports=[],
             hookspath=[],
             runtime_hooks=[],
             excludes=[],
             win_no_prefer_redirects=False,
             win_private_assemblies=False,
             cipher=block_cipher,
             noarchive=False)

pyz = PYZ(a.pure, a.zipped_data, cipher=block_cipher)

exe = EXE(pyz,
          a.scripts,
          a.binaries,
          a.zipfiles,
          a.datas,
          [],
          name='start_menu',  # 打包程序的名字
          debug=False,  
          bootloader_ignore_signals=False,  
          strip=False,  
          upx=True,  
          upx_exclude=[],  
          runtime_tmpdir=None,  
          console=True)  # console=True表示生成的可执行文件双击时会显示命令行窗口
          debug=False,
          bootloader_ignore_signals=False,
          strip=False,
          upx=True,
          upx_exclude=[],
          runtime_tmpdir=None,
          console=True)  # console=True表示生成的可执行文件双击时会显示命令行窗口
```

> **注**：如果想要修改程序图标，可以在 `EXE()` 中加入 `icon='xxxxx'`，请使用绝对路径。

#### 2.3 执行打包

在项目路径下执行以下指令以打包：

```bash
pyinstaller -F start_menu.spec
```

运行结束后，会新增 `dist` 文件夹，在该文件夹下，你将找到打包好的程序 `start_menu.exe`。

至此，打包结束。

---

## 附录

### 常见问题解决

1. **PyInstaller打包错误：`option(s) not allowed: --onedir/--onefile makespec options not valid`**
   - [解决方案链接](https://blog.csdn.net/dbfgngb/article/details/133935154)

2. **PyInstaller打包报错：`IndexError: tuple index out of range`**
   - [解决方案链接](https://blog.csdn.net/zuolixiangfisher/article/details/131570477)
   - 在 `vim` 编辑器中进入报错的文件 `/usr/local/lib/python3.10/dis.py`，找到 `def _unpack_opargs(code)` 函数，在 `else` 语句中添加 `extended_arg=0` 修复此问题。


## 使用Nuitka打包Python程序

### 简介

[Nuitka](https://nuitka.net/) 是一个将 Python 代码编译成独立可执行文件的工具。以下为使用 Nuitka 打包的详细步骤。

[Python——Windows使用Nuitka2.0打包（保姆级教程）](https://blog.csdn.net/Pan_peter/article/details/136411229)

[使用 Nuitka 打包 Python 脚本为独立的可执行文件](https://blog.csdn.net/craybb/article/details/144743012)

说明：下载mingw等工具耗时较长

---

### 一、Python虚拟环境搭建

#### 1.1 下载Python

访问 [Python官网](https://www.python.org/) 下载最新版的 Python 安装程序，并根据操作系统进行安装。

#### 1.2 使用venv创建虚拟环境

在命令行中，使用以下命令创建一个名为 `myenv` 的虚拟环境：

```bash
python -m venv myenv
```

激活虚拟环境：

```bash
# Linux或macOS
source myenv/bin/activate

# Windows
myenv\Scripts\activate.bat
```

#### 1.3 进入虚拟环境

激活虚拟环境后，命令行提示符会更改，以显示当前激活的虚拟环境名称。

#### 1.4 安装项目依赖包

建议将 `pip` 源更改为清华大学镜像站点，以加速下载。然后安装 Nuitka 和其他项目依赖包：

```bash
pip install nuitka
pip install -r requirements.txt  # 假设所有依赖都列在了requirements.txt文件中
```

### 二、使用Nuitka打包

#### 2.1 打包常用命令

Nuitka 的命令行参数非常灵活，根据需要选择合适的参数以满足不同的打包需求。以下是一个示例命令：

```bash
nuitka --mingw64 --show-progress --standalone --disable-console --enable-plugin=pyside6 --plugin-enable=numpy --onefile --remove-output camera.py
```

这个命令会使用 Nuitka 和 MinGW64 编译器来打包一个名为 `camera.py` 的 Python 项目。

- `--standalone` 选项会创建一个独立可执行文件。
- `--disable-console` 可用于 GUI 应用程序以隐藏命令行窗口。
- 可以根据项目需求启用其他插件，如 `pyside6` 和 `numpy`。
- `--onefile` 参数用于生成单个可执行文件。

#### 2.2 注意事项

- 确保所有需要的环境和工具已正确安装，包括适当版本的 MinGW 和相关依赖。
- 根据项目实际需求选择合适的 Nuitka 参数。
- 如果遇到问题，参阅[Nuitka官方文档](https://nuitka.net/doc/user-manual.html)或搜索相关错误信息获取帮助。

#### 2.3 打包成功

成功执行上述命令后，您的项目将被打包为一个可执行文件，位于指定的输出目录中。

如需了解更多信息，建议查看 Nuitka 的 [GitHub页面](https://github.com/Nuitka/Nuitka)，获取最新使用技巧和更新。

---

通过本教程，你应该能够熟练使用 PyInstaller 和 Nuitka 将 Python 脚本打包成可独立运行的可执行文件，以便于分发和使用。如果在使用过程中遇到任何问题，欢迎随时讨论或寻求帮助。

