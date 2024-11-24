---
layout: post
title: "linux下一键搭建SS"
date: 2018-05-04 23:28:00 +08:00
categories: ["笔记"]
tags: ["wget", "shadowsocks"]
---

事实上Ubuntu centos都可以使用此命令行
> wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
> chmod +x shadowsocks.sh 
> ./shadowsocks.sh 2>&1 | tee shadowsocks.log