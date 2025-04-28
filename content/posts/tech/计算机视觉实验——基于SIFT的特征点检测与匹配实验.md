---
title: "计算机视觉实验——基于SIFT的特征点检测与匹配实验"
date: 2025-04-29T00:02:25+08:00
lastmod: 2025-04-29T00:04:22+08:00
draft: false
math: true
categories:
- 计算机
- 编程
tags:
- 计算机视觉
- 特征点检测
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


# 实验名称

**特征点检测与匹配实验**

---

# 实验目的

- 理解并实践基于OpenCV的SIFT特征提取与匹配流程。
- 掌握特征点检测、描述符计算和匹配技术。
- 统计两张图像中提取的特征点数目，并绘制匹配前后的效果。
- 掌握两种常用匹配器：暴力匹配器（Brute-Force Matcher）和FLANN匹配器。

---

# 关键词详解

### SIFT（Scale-Invariant Feature Transform）

SIFT是一种经典的特征点检测与描述算法，能够检测出图像中的关键特征点，对尺度、旋转和亮度变化具有较强的健壮性。 它不仅找到特征点的位置，还计算其描述符，用于后续的匹配。

### BFMatcher（Brute-Force Matcher）

暴力匹配器，即遍历所有描述符，计算两两间的距离（相似度）来找到匹配对。参数`normType`决定距离计算方式，如`NORM_L2`适合SIFT特征。简单易用，适合小规模数据。

### FLANN（Fast Library for Approximate Nearest Neighbors）

快速近似最近邻搜索库，是一个大规模数据下更高效的匹配方案，相比暴力匹配速度更快。通过选择不同算法和搜索次数，可以在精确性与速度间做平衡。

---

# 实验环境配置

安装所需库：

```bash
conda install numpy
conda install opencv
conda install matplotlib
conda install jupyter
```

---

# 实验步骤

## 1. 导入相关包

```python
import numpy as np
import cv2
from matplotlib import pyplot as plt
```

## 2. 读取图像

使用两张部分重叠的照片，转为灰度图：

```python
img1 = cv2.imread('queryImage.png', 0)  # 查询图像
img2 = cv2.imread('trainImage.png', 0)  # 训练图像
```

## 3. SIFT特征提取

创建SIFT对象，并提取特征点及描述符：

```python
sift = cv2.xfeatures2d.SIFT_create()
kp1, des1 = sift.detectAndCompute(img1, None)
kp2, des2 = sift.detectAndCompute(img2, None)

print(f"图像1特征点数: {len(kp1)}")
print(f"图像2特征点数: {len(kp2)}")
```

## 4. 特征匹配

### 4.1 暴力匹配器（BFMatcher）

```python
bf = cv2.BFMatcher(normType=cv2.NORM_L2)

# KNN匹配，k=2返回每个点两个最佳匹配
matches = bf.knnMatch(des1, des2, k=2)

# Lowe比率测试，去除模糊匹配
good = []
for m, n in matches:
    if m.distance < 0.75 * n.distance:
        good.append([m])

# 绘制匹配结果
img3 = cv2.drawMatchesKnn(img1, kp1, img2, kp2, good, None, flags=2)
plt.imshow(img3)
plt.title('BFMatcher匹配结果')
plt.show()
```

**注意：**

- `normType=cv2.NORM_L2`适用于SIFT特征描述符。
- Lowe比率测试是为减少错误匹配。

### 4.2 FLANN匹配器

```python
FLANN_INDEX_KDTREE = 0

index_params = dict(algorithm=FLANN_INDEX_KDTREE, trees=5)
search_params = dict(checks=50)  # 检查次数，数值越大匹配越准确但速度变慢

flann = cv2.FlannBasedMatcher(index_params, search_params)
matches = flann.knnMatch(des1, des2, k=2)

good = []
for m, n in matches:
    if m.distance < 0.75 * n.distance:
        good.append([m])

img4 = cv2.drawMatchesKnn(img1, kp1, img2, kp2, good, None, flags=2)  
plt.imshow(img4)  
plt.title('FLANN匹配结果')  
plt.show()
```

---

## 5. 附加实验：计算单应矩阵，实现图像拼接

### 目的

根据上一步匹配的关键点，计算两幅图像间的单应矩阵（Homography），用于图像对齐与拼接。

### 原理

单应矩阵描述二维图像坐标之间的透视变换关系。计算后可以对原图进行透视变换，将两图平滑拼接。

### 实现步骤

```python
good_matches = []
for m, n in matches:
    if m.distance < 0.75 * n.distance:
        good_matches.append(m)

# 获取匹配点坐标
src_pts = np.float32([kp1[m.queryIdx].pt for m in good_matches]).reshape(-1, 1, 2)
dst_pts = np.float32([kp2[m.trainIdx].pt for m in good_matches]).reshape(-1, 1, 2)

# 计算单应矩阵，使用RANSAC算法提高鲁棒性
M, mask = cv2.findHomography(src_pts, dst_pts, cv2.RANSAC, 5.0)

# 读取原图
im_src = cv2.imread('queryImage.png')
im_dst = cv2.imread('trainImage.png')

# 利用单应矩阵进行透视变换，将 src 图映射到 dst 图坐标系
im_out = cv2.warpPerspective(im_src, M, (im_dst.shape[1], im_dst.shape[0]))

# 拼接显示：将变换后的src图与dst图并排显示
plot_image = np.concatenate((im_out, im_dst), axis=1)
plt.imshow(cv2.cvtColor(plot_image, cv2.COLOR_BGR2RGB))
plt.title('单应变换拼接效果')
plt.axis('off')
plt.show()
```

---

# 完整代码

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

MIN_MATCH_COUNT = 10

# Read Images
img1 = cv2.imread('D:\python\CV\dataset\images\IMG_20250428_085110.jpg', 1)
img1 = cv2.resize(img1, dsize=None, fx=0.6, fy=0.6, interpolation=cv2.INTER_LINEAR)     # 图像过大就缩小了再处理
img2 = cv2.imread('D:\python\CV\dataset\images\IMG_20250428_085120.jpg', 1)
img2 = cv2.resize(img2, dsize=None, fx=0.6, fy=0.6, interpolation=cv2.INTER_LINEAR)


# Create SIFT Object Initiate SIFT detector
sift = cv2.SIFT_create()

# Find the keypoints and descriptors with SIFT
kp1, des1 = sift.detectAndCompute(img1, None)
kp2, des2 = sift.detectAndCompute(img2, None)
# 输出检测到特征点的数量
print(f"Image 1 detected keypoints: {len(kp1)}")
print(f"Image 2 detected keypoints: {len(kp2)}")

# FLANN 匹配器
FLANN_INDEX_KDTREE = 1
index_params = dict(algorithm=FLANN_INDEX_KDTREE, trees=5)
search_params = dict(checks=50)   # or pass empty dictionary

flann = cv2.FlannBasedMatcher(index_params, search_params)

matches = flann.knnMatch(des1, des2, k=2)
# 输出匹配数目，应与size(des1)*k一致
print(f"Total FLANN matches: {len(matches)} (Expected ~{des1.shape[0] * 2})")

matchesMask = [[0,0] for i in range(len(matches))]

# ratio test as per Lowe's paper
valid_matches_count = 0
for i, (m, n) in enumerate(matches):
    if m.distance < 0.7 * n.distance:
        matchesMask[i] = [1, 0]
        valid_matches_count += 1

# 输出有效匹配的数目
print(f"Valid FLANN matches after ratio test: {valid_matches_count}")

# Draw
draw_params = dict(
    matchColor=(0, 255, 0),           # 绿色线条表示匹配点对
    singlePointColor=(255, 0, 0),     # 红色表示未匹配的点
    matchesMask=matchesMask,
    flags=cv2.DrawMatchesFlags_DEFAULT
)
img3 = cv2.drawMatchesKnn(img1, kp1, img2, kp2, matches, None, **draw_params)
plt.imshow(img3)
plt.show()


# BFMatcher 匹配器使用
bf = cv2.BFMatcher()
matches_bf = bf.knnMatch(des1, des2, k=2)
# 输出匹配数目
print(f"Total BF matches: {len(matches_bf)}")

# Apply ratio test
good = []
for m, n in matches_bf:
    if m.distance < 0.75 * n.distance:
        good.append([m])

# 输出好的点数目
print(f"Good BF matches after ratio test: {len(good)}")

img3 = cv2.drawMatchesKnn(img1, kp1, img2, kp2, good, None,
                         flags=cv2.DrawMatchesFlags_NOT_DRAW_SINGLE_POINTS)
cv2.imwrite(r'./result/bfmatcher.jpg', img3)
plt.imshow(img3)
plt.show()


# Compute Homography based on FLANN good matches
good = []
for m, n in matches:
    if m.distance < 0.7 * n.distance:
        good.append(m)

if len(good) > MIN_MATCH_COUNT:
    src_pts = np.float32([kp1[m.queryIdx].pt for m in good]).reshape(-1,1,2)
    dst_pts = np.float32([kp2[m.trainIdx].pt for m in good]).reshape(-1,1,2)
    M, mask = cv2.findHomography(src_pts, dst_pts, cv2.RANSAC, 5.0)
    # findHomography之后点数改变，输出RANSAC筛选的点数
    inliers = mask.ravel().tolist()
    print(f"Number of inliers after RANSAC: {np.sum(mask)}")
    matchesMask = inliers

    h, w = img1.shape[:2]  # 注意要取前两个维度 (高,宽)
    pts = np.float32([[0,0],[0,h-1],[w-1,h-1],[w-1,0]]).reshape(-1,1,2)
    dst = cv2.perspectiveTransform(pts, M)
    img2 = cv2.polylines(img2, [np.int32(dst)], True, 255, 3, cv2.LINE_AA)
else:
    print(f"Not enough matches are found - {len(good)}/{MIN_MATCH_COUNT}")
    matchesMask = None

draw_params = dict(
    matchColor=(0, 255, 0),
    singlePointColor=None,
    matchesMask=matchesMask,
    flags=2
)
img3 = cv2.drawMatches(img1, kp1, img2, kp2, good, None, **draw_params)
plt.imshow(img3, 'gray')
plt.show()


#比率测试
goods = []
for m, n in matches:
    if m.distance < 0.75 * n.distance:
        goods.append(m)

src_pts = np.float32([kp1[m.queryIdx].pt for m in goods]).reshape(-1, 1, 2)
dst_pts = np.float32([kp2[m.trainIdx].pt for m in goods]).reshape(-1, 1, 2)

M, mask = cv2.findHomography(src_pts, dst_pts, cv2.RANSAC, 5.0)

im_src = cv2.imread("D:\python\CV\dataset\images\IMG_20250428_085110.jpg")
im_dst = cv2.imread("D:\python\CV\dataset\images\IMG_20250428_085120.jpg")

im_out = cv2.warpPerspective(im_src, M, (im_dst.shape[1], im_dst.shape[0]))

plot_image = np.concatenate((im_out, im_dst), axis = 1)
plt.imshow(plot_image)
plt.show()
```

## 输出结果展示

```
Image 1 detected keypoints: 1184
Image 2 detected keypoints: 3594
Total FLANN matches: 1184 (Expected ~2368)
Valid FLANN matches after ratio test: 162
Total BF matches: 1184
Good BF matches after ratio test: 193
Number of inliers after RANSAC: 82
```

## 图片展示

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost05/img20250428235859.png)

该图为FLANN匹配结果。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost05/img20250428235926.png)

该图为暴力匹配结果。


![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost05/img20250429000004.png)

该图为基于FLANN good matches计算Homography的结果展示图。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost05/img20250429000017.png)

该图为两张有部分区域重叠图片拼接结果展示图。

单应矩阵描述二维图像坐标之间的透视变换关系。计算后可以对原图进行透视变换，将两图平滑拼接。

# 实验总结

- 成功提取了两张图像的局部不变特征点，统计了特征点数量。
- 使用暴力匹配和FLANN两种匹配器实现特征点匹配，掌握了关键参数和匹配策略。
- 学习了Lowe比率测试，有效过滤错误匹配。
- 通过计算单应矩阵实现了基于特征点的图像拼接，进一步理解了图像配准与变换的关系。

本实验助力理解特征点提取与匹配基本流程，为后续的图像识别、拼接和三维重建任务打下基础。

---

# 参考资料

- OpenCV官方文档 — SIFT: [https://docs.opencv.org/](https://docs.opencv.org/)
- Lowe D. G. “Distinctive Image Features from Scale-Invariant Keypoints”. IJCV. 2004.
- FLANN官方文档: [https://www.cs.ubc.ca/research/flann/](https://www.cs.ubc.ca/research/flann/)
- OpenCV中findHomography函数用法介绍









