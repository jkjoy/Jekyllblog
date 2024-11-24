---
layout: post
title: "Solidworks2013 VBA引擎崩溃问题解决"
date: 2018-07-03 19:06:48 +08:00
categories: ["笔记"]
---

<p>今天打开Solidworks2013时候加载VBA引擎时提示vbe6ext.olb不能被加载。</p>
<img src="https://mrwen.oss-cn-shanghai.aliyuncs.com/2018/07/w136h2319126_1444734785_583.jpg" alt="" />
<img src="https://mrwen.oss-cn-shanghai.aliyuncs.com/2018/07/w188h2319126_1444734775_256.jpg" alt="" />
<p>解决方法就是把
C:\Program Files（x86）\Common Files\Microsoft Shared\VBA\VBA7.1
目录下的vbe6ext.olb文件复制到
C:\Program Files\Common Files\Microsoft Shared\VBA\VBA7.1</p>
<p>重启Solidworks2013即可。</p>