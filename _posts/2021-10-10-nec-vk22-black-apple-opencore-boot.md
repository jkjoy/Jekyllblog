---
layout: post
title: "NEC VK22 黑苹果opencore引导"
date: 2021-10-10 15:42:00 +08:00
categories: ["分享"]
tags: ["文件", "苹果", "macos", "opencore", "efi", "笔记本", "clover", "edid", "注入", "hackintool"]
---

笔记本黑苹果的难点就在于注入edid。
我的思路是在clover下安装好macos之后再用hackintool注入EDID，然后再转为opencore引导。
其他都很简单我就不多说了。
附上EFI文件，三码自己改