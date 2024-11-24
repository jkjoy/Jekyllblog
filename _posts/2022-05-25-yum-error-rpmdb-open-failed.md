---
layout: post
title: "yum提示Error: rpmdb open failed 报错处理"
date: 2022-05-25 08:53:21 +08:00
categories: ["默认"]
---

宝塔面板安装docker失败时报错，可以使用以下方法重建rpm

# rpmdb所在目录

```bash
cd /var/lib/rpm
```

# 清除原rpmdb文件

```bash
rm -f __db.*
```

# 重建rpm数据库

```bash
rpm --rebuilddb
```

# 清除所有yum的缓存

```bash
yum clean all
```