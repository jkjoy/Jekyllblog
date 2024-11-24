---
layout: post
title: "在fly.io部署Memos并自动备份数据库"
date: 2023-08-15 10:02:00 +08:00
categories: ["分享"]
tags: ["memos", "部署", "fly.io"]
---

## 参考项目

https://github.com/hu3rror/memos-on-fly

## 准备工作

1.注册FLY.IO 
用以部署memos
2.注册B2C 
https://www.backblaze.com/cloud-storage
 用以同步备份memos数据库
 新建BUCKET,并获取`<keyId>`和`<applicationKey>`


## 安装flyctl
Install flyctl 
以WINDOWS为例
```
pwsh -Command "iwr https://fly.io/install.ps1 -useb | iex"
```
其他系统请参照官方

## 新建APP

初始化
```
flyctl launch
```
按照提示选择会生成一个FLY.TOML文件

## 编辑FLY.TOML

添加以下内容

```
[build]
  image = "ghcr.io/hu3rror/memos-litestream:latest"
#如果不需要备份数据库则可以选择官方的docker镜像ghcr.io/usememos/memos:latest
#使用官方镜像可以删掉env的部分
[env]
  # Details see: https://litestream.io/guides/backblaze/
  LITESTREAM_REPLICA_BUCKET = "B2C桶名称"     # change to your litestream bucket name
  LITESTREAM_REPLICA_ENDPOINT = "s3.us-east-005.backblazeb2.com"     # change to your litestream endpoint url
  LITESTREAM_REPLICA_PATH = "memos_prod.db"     # keep the default or change to whatever path you want

[[mounts]]
  source = "memos_data"
  destination = "/var/opt/memos"

[http_service]
  internal_port = 5230
  force_https = true
  auto_stop_machines = false
  auto_start_machines = true
  min_machines_running = 0
```

## 添加1g存储空间

```
flyctl volumes create memos_data --region hkg --size 1
```

## 添加密钥
将B2存储的密钥添加到fly的密钥存储中,
使用官方镜像可以忽略此步骤

```
flyctl secrets set LITESTREAM_ACCESS_KEY_ID="<keyId>" LITESTREAM_SECRET_ACCESS_KEY="<applicationKey>"
```

## 部署
执行
```
flyctl deploy
```
看到成功的提示可打开域名查看

## 演示地址

https://memosim.fly.dev/
绑定域名演示
https://imad.top

## 下载数据库
`fly.io`部署`artalk`或者`memos`后,使用SFTP下载SQLite 数据库

```
flyctl sftp get ./data/artalk.db #数据库路径
```
