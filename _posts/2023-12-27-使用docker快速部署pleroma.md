---
layout: post
title: "使用docker快速部署Pleroma实例"
date: 2023-12-27 18:44:00 +08:00
categories: ["分享"]
tags: ["docker", "Pleroma"]
---

## Pleroma是什么

Pleroma是一个联合社交网络平台，与GNU社交和其他OStatus实现兼容。它是AGPLv3许可下的免费软件。它实际上由两个组件组成:后端(名称简单为Pleroma)和面向用户的前端(名称为Pleroma-FE).它的主要优点是重量轻、速度快.

## 准备工作

* Docker

* git

## 步骤

### 拉取仓库

```bash
git clone https://github.com/jkjoy/docker-pleroma.git
cd docker-pleroma
```

### 创建文件夹并赋权

```bash

mkdir uploads config
chown -R 911:911 uploads
```

### Pleroma需要**citext** PostgreSQL拓展

```bash

docker-compose up -d db
docker exec -i pleroma_db psql -U pleroma -c CREATE EXTENSION IF NOT EXISTS citext;
docker-compose down
```

### 修改docker-compose.yml文件中的ENV内容

```yaml

DOMAIN: example.com   //实例使用的域名
INSTANCE_NAME: Pleroma  //实例的名称
ADMIN_EMAIL: admin@example.com //管理员邮箱
NOTIFY_EMAIL: notify@example.com //通知邮箱
DB_USER: pleroma  //可以保持默认
DB_PASS: ChangeMe! //可以保持默认
DB_NAME: pleroma //可以保持默认
```

保存好之后执行

```bash

docker-compose up -d
```

### 查看容器的状态

```bash

docker logs -f pleroma_web
```

### 反向代理

反向代理127.0.0.1:4000以宝塔为例 ![](https://www.imsun.org/usr/uploads/2023/12/QQ截图20231227190251.png)

### 创建一个管理员账号

以下示例中 fakeadmin 为用户名 admin@test.net 为邮箱

```bash

docker exec -it pleroma_web sh ./bin/pleroma_ctl user new fakeadmin admin@test.net --admin
```

执行之后会出现一个链接,点击即可重置管理员密码 ### 更改前端

Pleroma-FE不太喜欢,选用 Soapbox作为前端

```bash

cd static
curl -O https://dl.soapbox.pub/main/soapbox.zip
```

```bash

unzip soapbox.zip
```

刷新即可

### 演示地址

[https://tot.yt](https://tot.yt)