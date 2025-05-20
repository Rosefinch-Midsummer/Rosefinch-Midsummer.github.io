---
title: "使用 Vue 3 + Vite 结合 vue-gallery 创建响应式图片画廊并实现从文本文件读取图片 URL"
date: 2025-05-20T12:34:25+08:00
lastmod: 2025-05-20T12:54:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- 画廊
- Vue
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


# 使用 Vue 3 + Vite 结合 vue-gallery 创建响应式图片画廊并实现从文本文件读取图片 URL

## 前言

在现代 Web 项目中，展示图片画廊是一项常见需求。`vue-gallery` 是一个基于 Vue 的响应式、可定制的图片和视频画廊组件，内置轮播和灯箱效果，支持移动端和桌面端。

这篇文章将介绍如何：

- 使用 Vite 创建 Vue 3 项目
- 集成 `vue-gallery` 组件
- 实现从本地文本文件读取图片 URL，实现动态显示画廊图片

---

## 一、快速创建 Vue 3 + Vite 项目

Vite 是一个现代前端构建工具，非常适合 Vue3 开发。

```bash
npm create vite@latest vue-gallery-demo --template vue
cd vue-gallery-demo
npm install
npm run dev
```

项目启动成功后，我们即可开始集成 `vue-gallery`。

---

## 二、安装并引入 vue-gallery

目前 `vue-gallery` 主要面向 Vue 2，但官方源码兼容性较好，我们使用 Vue 3 项目时，需稍作调整或直接使用 Vue 2 版本的兼容方案。

示例中，我们使用 npm 安装：

```bash
npm install vue-gallery
# 或使用 yarn
yarn add vue-gallery
```

---

## 三、基础用法示例

创建一个简单的图片画廊组件 `Gallery.vue`：

```vue
<template>
  <div>
    <gallery 
      :images="images" 
      :index="index" 
      @close="index = null">
    </gallery>

    <div 
      v-for="(image, i) in images" 
      :key="i"
      class="image"
      @click="index = i"
      :style="{ backgroundImage: 'url(' + image + ')', width: '300px', height: '200px' }">
    </div>
  </div>
</template>

<script>
import VueGallery from 'vue-gallery'

export default {
  components: { gallery: VueGallery },
  data() {
    return {
      images: [
        'https://dummyimage.com/800/ffffff/000000',
        'https://dummyimage.com/1600/ffffff/000000',
        'https://dummyimage.com/1280/000000/ffffff',
        'https://dummyimage.com/400/000000/ffffff',
      ],
      index: null
    }
  }
}
</script>

<style scoped>
.image {
  float: left;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  border: 1px solid #ebebeb;
  margin: 5px;
  cursor: pointer;
}
</style>
```

上述代码实现基本功能：

- `images` 数组定义图片 URL
- 点击缩略图时触发灯箱打开
- 画廊关闭时，重置打开索引

---

## 四、从文本文件加载图片 URL

我们希望画廊的 `images` 数据，能动态从一个简单的 `.txt` 文件中读取，文件格式示例如下，每行一个图片 URL：

```
https://dummyimage.com/800/ffffff/000000
https://dummyimage.com/1600/ffffff/000000
https://dummyimage.com/1280/000000/ffffff
https://dummyimage.com/400/000000/ffffff
```

### 1. 将文本文件放入 public 目录

在 `public` 文件夹里放置 `images.txt`

```
public/images.txt
```

内容为上面所示的多行图片链接。

确保项目根目录中有一个 `public` 文件夹，且你的 `images.txt` 文件放在 `public/` 中：

```
project-root/
├─ public/
│  └─ images.txt   <- 这里
├─ src/
│  └─ components/
│     └─ Gallery.vue
├─ index.html
├─ package.json
```

> **注意：** Vite 在开发和构建时，`public` 中的静态资源会被原样复制，你的文件会在 `/images.txt` 路径正确访问。

### 2. 使用 Fetch API 读取文本

更新组件代码，实现动态加载：

```vue
<template>
  <div>
    <gallery 
      :images="images" 
      :index="index" 
      @close="index = null">
    </gallery>

    <div 
      v-for="(image, i) in images" 
      :key="i"
      class="image"
      @click="index = i"
      :style="{ backgroundImage: 'url(' + image + ')', width: '300px', height: '200px' }">
    </div>
  </div>
</template>

<script>
import VueGallery from 'vue-gallery'

export default {
  components: { gallery: VueGallery },
  data() {
    return {
      images: [],
      index: null
    }
  },
  mounted() {
    fetch('/images.txt')
      .then(res => res.text())
      .then(text => {
        this.images = text.split('\n').map(line => line.trim()).filter(line => line)
      })
      .catch(err => {
        console.error('Failed to load image URLs:', err)
      })
  }
}
</script>

<style scoped>
.image {
  float: left;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  border: 1px solid #ebebeb;
  margin: 5px;
  cursor: pointer;
}
</style>
```

这样，图片 URL 就会从 `public/images.txt` 文件动态读取，赋值给 `images` 数组，实现画廊展示。

---

## 五、完整代码

### App.vue

```vue
<script setup lang="ts">
import Gallery from './components/Gallery.vue'
</script>

<template>
  <Gallery/>
</template>
```

### Gallery.vue

```vue
<template>
  <div>
    <gallery
      :images="images"
      :index="index"
      @close="index = null">
    </gallery>

    <div
      v-for="(image, i) in images"
      :key="i"
      class="image"
      @click="index = i"
      :style="{ backgroundImage: 'url(' + image + ')', width: '300px', height: '200px' }">
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import VueGallery from 'vue-gallery'

const images = ref<string[]>([])
const index = ref<number | null>(null)

onMounted(() => {
  fetch('/images.txt')
    .then(res => {
      if (!res.ok) throw new Error(`HTTP error! Status: ${res.status}`)
      return res.text()
    })
    .then(text => {
      images.value = text.split('\n').map(line => line.trim()).filter(line => line)
    })
    .catch(err => console.error('Failed to load images:', err))
})
</script>

<script lang="ts">
export default {
  components: { gallery: VueGallery }
}
</script>

<style scoped>
.image {
  float: left;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
  border: 1px solid #ebebeb;
  margin: 5px;
  cursor: pointer;
}
</style>
```


## 六、总结与扩展

- **集成`vue-gallery`** 非常简便，支持多平台响应式。
- **文本文件加载** 利用浏览器 Fetch API 简单实现了数据动态获取，无需复杂后端支持。
- 如果你需要支持复杂的 EXIF 图片旋转问题，也可以参考 `vue-gallery` 的 `onslide` 回调进行处理，保证图片方向正确。
- 在 Vue 3 + Vite 项目中使用 Vue 2 组件时，注意兼容性问题，必要时可封装或改造组件。

---

## 参考链接

- [vue-gallery npm 页面](https://www.npmjs.com/package/vue-gallery)
- [Vite 官网](https://vitejs.dev/)
- [关于 EXIF 图片旋转的问题](https://stackoverflow.com/questions/20600800/js-client-side-exif-orientation-rotate-and-mirror-jpeg-images)
- [Demo jsFiddle](https://jsfiddle.net/orotemo/obvna6qn/)



















