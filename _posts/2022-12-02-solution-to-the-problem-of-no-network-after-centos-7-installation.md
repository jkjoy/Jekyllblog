---
layout: post
title: "centos7安装后没有网络的解决办法"
date: 2022-12-02 13:43:00 +08:00
categories: ["测试"]
---

以`root`账号登陆
用`ip addr`命令查看网络参数。
打开`eth0`网卡的配置文件`/etc/sysconfig/network-scripts/ifcfg-eth0`，把`NOBOOT`参数`no`，修改为`yes`。
`重启网络`或者`重启服务器`都可

