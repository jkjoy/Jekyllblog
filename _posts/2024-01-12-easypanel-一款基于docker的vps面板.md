---
layout: post
title: "EasyPanel：一款基于Docker的VPS面板"
date: 2024-01-12 15:08:00 +08:00
categories: ["分享"]
tags: ["docker", "EasyPanel", "gatus"]
---

## EasyPanel

官方网站 `EasyPanel.io` `EasyPanel`是一款基于`docker`的可视化面板. 拥有`付费`和`免费`两种模式

本文介绍以免费模式为主(主要是收费不菲) 
![](https://www.imsun.org/usr/uploads/2024/01/20240112071321641777.webp)

从首页的介绍可以看到他的特色就是通过直观的界面部署应用,管理数据库以及签发SSL证书.

### 安装

+   建议在纯净的linux系统下安装

通过命令行

```sh
curl -sSL https://get.easypanel.io | sh
```

即可完成安装,官方给出的配置要求内存大于2G,根据实测,1G的vps运行起来问题也不大.

由于是容器化的部署方式,各个应用之间独立运行.NICE.

### 使用

#### 访问

安装之后通过

```auto
ip:3000
```

访问面板,初次访问会要求创建管理员账号和密码.

#### 登录

进入面板会发现很简洁 
![进入面板](https://www.imsun.org/usr/uploads/2024/01/20240112073049083915.webp)

#### 创建

创建项目点击`Create Project`填写项目名称,确定,进入该项目

#### 模板

![](https://www.imsun.org/usr/uploads/2024/01/20240112074114481559.webp)

点击`templates`会发现这里有很多常用的应用模板,只要点击就可以部署.

譬如`memos` `uptime` `wordpress` `Flarum` `GoToSocial` `Umami` `Vaultwarden` 等上百款应用

#### 服务

常见的模板应用大多都是全世界著名的应用.国内的某些应用,或者不是很常见的应用该如何部署

此处以`gatus`为例

![](https://www.imsun.org/usr/uploads/2024/01/20240112074948886487.webp) 

点击`APP`,填写名称,确认 

![](https://www.imsun.org/usr/uploads/2024/01/20240112075045277316.webp) 

点击`General`
`gatus`的docker镜像为`twinproduction/gatus:latest`
在`Docker images`中填入`twinproduction/gatus:latest`
点`SAVE`保存. 
![](https://www.imsun.org/usr/uploads/2024/01/20240112075239607243.webp) 
点击`Domain`\-`ADD Domain`\-`HOST`填写域名

![](https://www.imsun.org/usr/uploads/2024/01/20240112075722912648.webp)

全部填写完成之后,点`SAVE`保存. 

![](https://www.imsun.org/usr/uploads/2024/01/20240112080453993746.webp) 

点击`Advanced`\-`Mounts`\-`ADD VOLUME Mounts` 

`Name`为宿主机名称可以自己设置 

`Mount Path`为Docker

挂载目录 `/data`

点击`ADD File Mounts`,其中 `Mount Path`为挂载路径,此处填写为`/config/config.yaml` 

`Content`为yaml格式的配置文件 与 `config.yaml`内容对应 

以下为示例内容可自行修改

```yaml
storage:
  type: sqlite
  path: /data/data.db

ui:
  buttons:
    - name: "Home"
      link: "https://www.imsun.org"

endpoints:
  - name: bloghb
    group: core
    url: "https://blog.hb.cn"
    interval: 3m
    conditions:
      - "[STATUS] == 200"

  - name: blogcn
    group: core
    url: "https://blog.asbid.cn"
    interval: 3m
    conditions:
      - "[STATUS] == 200"

  - name: blogsd
    group: core
    url: "https://blog.sd.cn"
    interval: 3m
    conditions:
      - "[STATUS] == 200"
```

点击`SAVE`保存 

![](https://www.imsun.org/usr/uploads/2024/01/20240112081537297595.webp)

点击`Deploy`. 

完成部署 别忘记在DNS处解析域名

### gatus演示

[https://status.0tz.top/](https://status.0tz.top/)

## 总结

优势:不用折腾反代,不用担心证书到期,常用应用傻瓜式部署