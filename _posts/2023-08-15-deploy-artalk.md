---
layout: post
title: "在fly.io部署artalk评论系统"
date: 2023-08-15 09:37:00 +08:00
categories: ["分享"]
tags: ["部署", "fly.io", "artalk"]
---

众所周知`Fly.io`是一个免费的SAAS平台
提供三个内存为256MB,总3G硬盘空间.
为防止滥用,需要绑定信用卡.
```
Free allowances
Resources included for free on all plans:

Up to 3 shared-cpu-1x 256mb VMs†
3GB persistent volume storage (total)
160GB outbound data transfer
```
## 准备
安装官方的命令行工具flyctl

## 初始化
```bash
flyctl launch
```
根据提示创建一个app

## 创建一个1G的硬盘
1G的硬盘用来储存评论数据绰绰有余了
```yaml
flyctl volumes create artalk_data --region hkg --size 1
```
## 编辑FLY.TOML

```yaml
#根据自动生成的FLY.TOML文件修改
app = "atim"  
primary_region = "hkg"

[build]
  image = "artalk/artalk-go"

[http_service]
  internal_port = 23366
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 0
  processes = ["app"]

[[mounts]]
  source = "artalk_data"
  destination = "/data"

[experimental]
  vm = true
```
## 在 fly.toml 文件目录执行
```bash
flyctl ssh console
```
创建一个管理员账号
```bash
./artalk admin
```
如需重启则执行
```bash
flyctl apps restart
```
## 上传IP数据库ip2region.xdb
`fly.io`部署`artalk`后,连接SFTP上传`ip2region.xdb`到`data`目录中
以下在FLY.TOML根目录下执行
```bash
flyctl sftp shell
cd data
put ip2region.xdb
```
等待上传
在`artalk`后台中设置路径`./data/ip2region.xdb`即可.

## 使用SFTP下载SQLite 数据库

```bash
flyctl sftp get ./data/artalk.db #数据库路径
```
