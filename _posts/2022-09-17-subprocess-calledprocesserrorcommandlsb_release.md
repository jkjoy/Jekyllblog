---
layout: post
title: "subprocess.CalledProcessError: Command '('lsb_release', '-a')' returned non-zero exit status 1."
date: 2022-09-17 10:11:00 +08:00
categories: ["默认"]
---

这个时候运行pip3 时出现了问题： 
>subprocess.CalledProcessError: Command \\'(\\'lsb\_release\\', \\'-a\\')\\' returned non-zero exit status 1.
## 解决办法
运行
```auto
sudo rm /usr/bin/lsb_release
```