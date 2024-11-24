---
layout: post
title: "黑苹果开机出现error loading kernel cache 0x1"
date: 2019-07-29 22:05:02 +08:00
categories: ["笔记"]
tags: ["论坛", "命令", "安装", "错误", "原因", "系统", "google", "办法", "苹果", "终端", "macos", "volumes", "分区", "kextcache", "library", "system"]
---

出现这个错误的原因是系统缓存出现错误
在google上看到国外黑苹果论坛给出了解决办法

进入苹果安装盘
打开终端工具   命令行
df -h

touch /Volumes/macOS安装分区/System/Library/Extensions && kextcache -u /Volumes/macOS安装分区
注意macOS安装分区名称如果有空格记得在后面加“\”
会出现提示
Child process [directory] has exited due to signal 10

Error 107 rebuilding /System/Library/PrelinkedKernels/prelinkedkernel
删除他们
rm -f /Volumes/macOS安装分区/System/Library/PrelinkedKernels/prelinkedkernel