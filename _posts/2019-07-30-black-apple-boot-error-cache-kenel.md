---
layout: post
title: "黑苹果开机出现error loading kernel cache 0x1"
date: 2019-07-30 06:05:02 +08:00
categories: ["默认"]
---

<p>出现这个错误的原因是系统缓存出现错误<br />在google上看到国外黑苹果论坛给出了解决办法</p><p>进入苹果安装盘<br />打开终端工具   命令行<br />df -h</p><p>touch /Volumes/macOS安装分区/System/Library/Extensions && kextcache -u /Volumes/macOS安装分区<br />注意macOS安装分区名称如果有空格记得在后面加“\”<br />会出现提示<br />Child process [directory] has exited due to signal 10</p><p>Error 107 rebuilding /System/Library/PrelinkedKernels/prelinkedkernel<br />删除他们<br />rm -f /Volumes/macOS安装分区/System/Library/PrelinkedKernels/prelinkedkernel</p>