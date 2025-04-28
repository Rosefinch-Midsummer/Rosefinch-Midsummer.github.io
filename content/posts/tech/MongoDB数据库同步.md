---
title: "MongoDB 数据库同步"
date: 2025-04-28T18:34:25+08:00
lastmod: 2025-04-28T22:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- 数据库
- MongoDB
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

为了实现数据在本地 MongoDB 和 MongoDB Atlas 之间的同步，同时避免 `DuplicateKeyError` (E11000) 错误，我们需要按照以下要求编写三个 Python 脚本：

1. **清空指定集合中的所有数据。**
2. **将本地数据迁移到 Atlas MongoDB，避免重复键，并记录重复的键。**
3. **将 Atlas MongoDB 数据迁移到本地，避免重复键，并记录重复的键。**

以下是实现这三个脚本的代码：

## 1. 清空指定集合中的所有数据

```python
from pymongo import MongoClient

def clear_collection(collection_name):
    # 本地MongoDB连接
    local_client = MongoClient("mongodb://localhost:27017/")
    local_db = local_client['CourseRec']
    
    # 获取指定集合
    collection = local_db[collection_name]
    
    # 删除所有数据
    result = collection.delete_many({})
    print(f"已清空集合 '{collection_name}'，删除文档数量: {result.deleted_count}")

# 调用函数，清空集合
clear_collection("websites")
```

## 2. 将本地数据迁移到 Atlas MongoDB（过滤相同键）

```python
from pymongo import MongoClient, errors

# 替换为你的 MongoDB Atlas 的 URI
mongodb_uri = ""  # 这里填写你的 MongoDB URI

def migrate_local_to_atlas(collection_name):
    # 本地MongoDB连接
    local_client = MongoClient("mongodb://localhost:27017/")
    local_db = local_client['CourseRec']
    
    # MongoDB Atlas连接
    atlas_client = MongoClient(mongodb_uri)
    atlas_db = atlas_client['CourseRec']
    
    local_collection = local_db[collection_name]
    atlas_collection = atlas_db[collection_name]
    
    # 获取本地集合的所有文档
    local_documents = local_collection.find()

    for document in local_documents:
        try:
            # 尝试插入文档到Atlas
            atlas_collection.insert_one(document)
        except errors.DuplicateKeyError:
            print(f"文档ID '{document['_id']}' 重复，跳过该文档。")
        except Exception as e:
            print(f"插入文档时出现错误: {e}")

    print(f"本地集合 '{collection_name}' 的数据已成功迁移到 Atlas。")

# 调用函数进行迁移
migrate_local_to_atlas("websites")
```

## 3. 将 Atlas MongoDB 数据迁移到本地（过滤相同键）

```python
from pymongo import MongoClient, errors

# 替换为你的 MongoDB Atlas 的 URI
mongodb_uri = ""  # 这里填写你的 MongoDB URI

def migrate_atlas_to_local(collection_name):
    # 本地MongoDB连接
    local_client = MongoClient("mongodb://localhost:27017/")
    local_db = local_client['CourseRec']
    
    # MongoDB Atlas连接
    atlas_client = MongoClient(mongodb_uri)
    atlas_db = atlas_client['CourseRec']
    
    local_collection = local_db[collection_name]
    atlas_collection = atlas_db[collection_name]
    
    # 获取 Atlas 中的所有文档
    atlas_documents = atlas_collection.find()

    for document in atlas_documents:
        try:
            # 尝试插入文档到本地
            local_collection.insert_one(document)
        except errors.DuplicateKeyError:
            print(f"文档ID '{document['_id']}' 在本地已存在，跳过该文档。")
        except Exception as e:
            print(f"插入文档时出现错误: {e}")

    print(f"Atlas 集合 '{collection_name}' 的数据已成功迁移到本地。")

# 调用函数进行迁移
migrate_atlas_to_local("websites")
```

## 说明

- **清空集合**：`clear_collection` 函数会使用 `delete_many` 方法删除指定集合中的所有数据。
- **数据迁移**：
    - 在 `migrate_local_to_atlas` 和 `migrate_atlas_to_local` 函数中，使用 `insert_one` 方法尝试插入数据，并使用 `DuplicateKeyError` 异常处理来跳过已存在的文档。
    - `except Exception as e:` 语句用于捕获其他可能的异常，以便在发生错误时能够知道具体情况。

## 使用方法

为了使用这些脚本，你需要：

1. 先运行清空集合的脚本，以便在本地或 Atlas 中清理旧数据。
2. 然后运行相应的迁移脚本，实现数据的单向迁移。

确保你在运行这些脚本之前已经设定好MongoDB Atlas的连接URI和本地MongoDB的连接。根据你的项目需要，结合这些脚本来完成数据的同步与管理。







