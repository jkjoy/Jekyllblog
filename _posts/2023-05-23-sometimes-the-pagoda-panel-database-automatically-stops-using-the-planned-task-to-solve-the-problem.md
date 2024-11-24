---
layout: post
title: "宝塔面板数据库有时候自动停止用计划任务来解决的办法"
date: 2023-05-23 14:59:40 +08:00
categories: ["测试"]
tags: ["宝塔", "数据库", "mysql"]
---

创建计划任务,每分钟执行一次
脚本如下

```
pgrep -x mysqld &> /dev/null
if [ $? -ne 0 ];then
/etc/init.d/mysqld start 
fi
```
检测数据库状态并自动启动