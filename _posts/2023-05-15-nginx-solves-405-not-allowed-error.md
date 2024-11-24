---
layout: post
title: "nginx 解决 405 not allowed错误"
date: 2023-05-15 10:36:20 +08:00
categories: ["分享"]
tags: ["时光机", "nginx"]
---

## 问题出现
在使用时光机的微信公众号发布说说时,后台提示405错误!
这是之前从没有出现过的错误~

Apache、IIS、Nginx等绝大多数web服务器，都不允许静态文件响应POST请求，否则会返回“HTTP/1.1 405 Method not allowed”错误。

## 解决办法
在网上搜索到一个最简单的办法
在Nginx设置中加入
```
 error_page 405 =200 http://$host$request_uri;
```
即可解决