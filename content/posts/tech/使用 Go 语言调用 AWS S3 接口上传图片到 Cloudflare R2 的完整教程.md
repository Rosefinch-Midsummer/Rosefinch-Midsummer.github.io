---
title: "使用 Go 语言调用 AWS S3 接口上传图片到 Cloudflare R2 的完整教程"
date: 2025-05-17T19:34:25+08:00
lastmod: 2025-05-17T22:54:22+08:00
draft: false
math: true
categories:
- 编程
- 计算机
tags:
- Go
- CloudFlare
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

# 使用 Go 语言调用 AWS S3 接口上传图片到 Cloudflare R2 的完整教程

Cloudflare R2 兼容 AWS S3 的 API，因此我们可以使用 Go 语言结合 AWS 官方 SDK 来操作 R2，实现图片上传等功能。本文将详细介绍如何用 Go 调用 AWS SDK v2，通过 S3 接口将本地图片上传到 Cloudflare R2，并且讲解常见错误及解决方法。

---

## 步骤概览

1. **准备 R2 账户信息**  
    获取 R2 的 Endpoint、Access Key 和 Secret Key。注意，R2 的 Endpoint 与 AWS S3 不同，通常格式为：
    
    ```
    https://<account_id>.r2.cloudflarestorage.com
    ```
    
    Bucket 不同于 Endpoint，是在请求路径中指定的。
    
2. **在 Go 项目中引入 AWS SDK v2**  
    使用 Go 语言官方 AWS SDK v2，并配置为访问 R2 的 Endpoint。
    
3. **实现图片上传逻辑**
    
    - 读取本地图片文件
    - 配置客户端，强制使用路径风格（Path-style）访问
    - 调用 `PutObject` 接口完成上传操作

---

## 依赖安装

```bash
go get github.com/aws/aws-sdk-go-v2
go get github.com/aws/aws-sdk-go-v2/config
go get github.com/aws/aws-sdk-go-v2/credentials
go get github.com/aws/aws-sdk-go-v2/service/s3
```

---

## 代码示例

下面是一份可运行的完整示例，实现把本地图片上传到 Cloudflare R2。

```go
package main

import (
	"context"
	"fmt"
	"log"
	"os"

	"github.com/aws/aws-sdk-go-v2/aws"
	"github.com/aws/aws-sdk-go-v2/config"
	"github.com/aws/aws-sdk-go-v2/credentials"
	"github.com/aws/aws-sdk-go-v2/service/s3"
	"github.com/aws/aws-sdk-go-v2/service/s3/types"
)

func main() {
    // 替换以下参数为你自己的 R2 账号信息和文件路径
    endpoint := "https://<account_id>.r2.cloudflarestorage.com" // R2 Endpoint，注意是账号级别
    region := "auto"                                            // R2 region 可以随意写，通常写 "auto"
    accessKeyID := "<your_access_key>"
    secretAccessKey := "<your_secret_key>"
    bucket := "<your_bucket_name>"          // 你的桶名
    key := "example-image.jpg"              // 上传到 R2 后保存的文件名
    imagePath := "./example-image.jpg"      // 本地图片路径

    // 打开本地文件
    file, err := os.Open(imagePath)
    if err != nil {
        log.Fatalf("打开文件失败: %v", err)
    }
    defer file.Close()

    // 自定义 Endpoint 解析器，指定使用 R2 的 Endpoint
    resolver := aws.EndpointResolverFunc(func(service, region string) (aws.Endpoint, error) {
        if service == "s3" {
            return aws.Endpoint{
                URL:           endpoint,
                SigningRegion: region,
            }, nil
        }
        return aws.Endpoint{}, fmt.Errorf("未知服务: %s", service)
    })

    // 加载配置，填入 Region、静态凭证以及自定义 Endpoint 解析器
    cfg, err := config.LoadDefaultConfig(context.TODO(),
        config.WithRegion(region),
        config.WithCredentialsProvider(credentials.NewStaticCredentialsProvider(accessKeyID, secretAccessKey, "")),
        config.WithEndpointResolver(resolver),
    )
    if err != nil {
        log.Fatalf("加载 SDK 配置失败: %v", err)
    }

    // 创建 S3 客户端，强制使用路径风格（Path-style）访问，避免 TLS 握手错误
    client := s3.NewFromConfig(cfg, func(o *s3.Options) {
        o.UsePathStyle = true
    })

    // 调用 PutObject 上传文件
    _, err = client.PutObject(context.TODO(), &s3.PutObjectInput{
        Bucket:      aws.String(bucket),
        Key:         aws.String(key),
        Body:        file,
        ContentType: aws.String("image/jpeg"),                // 根据实际类型设置 Content-Type
        ACL:         types.ObjectCannedACLPublicRead,         // 如需公开访问，可设置 PublicRead，默认私有
    })
    if err != nil {
        log.Fatalf("上传失败: %v", err)
    }

    fmt.Println("文件上传成功！")
}
```

---

## 关键点解析

- **Endpoint**  
    Cloudflare R2 Endpoint 是账号级别的 URL，不是 Bucket 级的。形如：  
    `https://<account_id>.r2.cloudflarestorage.com`  
    Bucket 名作为路径的一部分放入请求中，而非子域名。
    
- **Path-style 访问**  
    AWS SDK 默认会把 Bucket 当作二级域（virtual hosted-style），例如 `bucket.endpoint`。Cloudflare R2 目前只支持路径风格访问，即：
    
    ```
    https://endpoint/bucket/key
    ```
    
    因此需在 S3 客户端中添加：
    
    ```go
    o.UsePathStyle = true
    ```
    
    这一步非常关键，避免出现 TLS 握手失败的错误。
    
- **Region**  
    R2 并不严格限定 Region，你可以写成 `"auto"` 或 `"us-east-1"` 不影响使用。
    
- **权限设置**  
    默认桶是私有的，如要公开访问可以设置 `ACL` 为 `public-read`。
    
- **Content-Type**  
    上传时指定正确的 Content-Type ，让浏览器或者客户端正确识别文件类型。
    

---

## TLS 握手失败问题排查

如果遇到类似下面的错误：

```
request send failed, Put "https://<bucket>.<account_id>.r2.cloudflarestorage.com/example-image.png?x-id=PutObject": remote error: tls: handshake failure
```

请注意：

1. **Endpoint 配置是否正确**  
    确保使用正确格式的 Endpoint，是账号 ID 作为子域，而不是 Bucket 名。
    
2. **UsePathStyle 是否启用**  
    AWS SDK 默认使用虚拟托管式（virtual-hosted-style）导致 Host 不匹配，必须设置 `UsePathStyle = true`。
    
3. **TLS 环境**  
    检查 Go 版本是否足够新（建议 Go 1.18+），以及网络环境没有使用代理或拦截 HTTPS。
    

---

## 总结

- 使用 Go 调用 AWS SDK v2 操作 Cloudflare R2，关键是正确配置 Endpoint 和强制路径风格访问
- 代码中需加载自定义 Endpoint 解析器，并指定路径风格访问才能避免 TLS 错误
- 上传时指定文件的 Content-Type 和权限控制，满足业务需求

希望这篇教程能够帮助你顺利用 Go 语言上传图片至 Cloudflare R2。













