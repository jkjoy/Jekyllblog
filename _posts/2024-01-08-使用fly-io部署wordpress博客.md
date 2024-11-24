---
layout: post
title: "使用fly.io部署wordpress博客"
date: 2024-01-08 15:56:00 +08:00
categories: ["分享"]
tags: ["wordpress"]
---

## 关于fly.io
 认证国际信用卡之后可以免费试用三个256MB内存的服务,以及3G的持久化存储 

## 使用docker镜像
 jkjoy/wordpress-sqlite-nginx 本次使用的镜像是基于nginx+php8.2+sqlite构建的 

## 准备
 flyctl-cli命令行工具 
[Install the CLI](https://fly.io/docs/hands-on/install-flyctl/) 

## 具体步骤
 登录 

```sh
flyctl auth login
```
 创建初始化APP 

```javascript
flyctl launch --name YOURAPPNAME --image=jkjoy/wordpress-sqlite-nginx:latest --region hkg --no-deploy
```
 创建1G持久化存储 

```sh
flyctl volumes create social_data --region hkg --size 1
```

## 编辑配置
 参照以下配置修改根目录下的fly.toml 

```yaml

app = "jkjoy"
primary_region = "hkg"

[build]
  image = "jkjoy/wordpress-sqlite-nginx"

[[mounts]]
  source = "conf_data"
  destination = "/usr/share/nginx/html/wp-content/database"
  auto_extend_size_threshold = 0

[http_service]
  internal_port = 80
  force_https = true
  auto_stop_machines = false
  auto_start_machines = true
  min_machines_running = 0
  processes = ["app"]

[[vm]]
  cpu_kind = "shared"
  cpus = 1
  memory_mb = 256
```
 以下路径 `/usr/share/nginx/html/wp-content/database`为数据库目录,挂载在1G持久化存储下. 

## 部署
 执行 

```sh
flyctl deploy
```
 启动成功后会显示一个URL,能成功访问则代表部署成功。 

## 赋权
 连接SSH 在根目录下执行 

```sh
flyctl ssh console
```
 连接成功后,执行 

```sh
chmod 0777 /usr/share/nginx/html/wp-content/database
```
 运行安装即可. 

## 演示
[https://jkjoy.fly.dev/](https://jkjoy.fly.dev/)