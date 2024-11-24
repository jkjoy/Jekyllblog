---
layout: post
title: "Solidworks2013 VBA引擎崩溃问题解决"
date: 2018-07-03 19:06:48 +08:00
categories: ["笔记"]
---

今天打开Solidworks2013时候加载VBA引擎时提示vbe6ext.olb不能被加载。

![Solidworks2013](https://mrwen.oss-cn-shanghai.aliyuncs.com/2018/07/w136h2319126_1444734785_583.jpg) 
![Solidworks2013](https://mrwen.oss-cn-shanghai.aliyuncs.com/2018/07/w188h2319126_1444734775_256.jpg)

解决方法就是把 `C:\\Program Files（x86）\\Common Files\\Microsoft Shared\\VBA\\VBA7.1` 目录下的`vbe6ext.olb`文件复制到 `C:\\Program Files\\Common Files\\Microsoft Shared\\VBA\\VBA7.1`

重启Solidworks2013即可。