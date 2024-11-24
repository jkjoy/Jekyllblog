---
layout: post
title: "Memos 0.13缩略图不显示的问题"
date: 2023-05-20 14:59:00 +08:00
categories: ["测试"]
tags: ["memos"]
---

## Memos
最新更新了版本
于是在本地用docker拉取了最新镜像看看是不是还有OSS无法上传的问题
## 测试
- 演示地址
https://demo.memos.im #本地服务器部署,有可能因为停电,断网等情况无法访问.

本地上传之后缩略图不显示
## 解决办法
在`root/.memos/`目录下新建`.thumbnail_cache`文件夹即可.
我猜测是因为没有权限建立文件夹造成的.
所以可能这个问题只存在于最新部署的memos上
## 结果
S3储存的OSS和COS还是无法上传,所以
建议使用0.11版本的memos.
