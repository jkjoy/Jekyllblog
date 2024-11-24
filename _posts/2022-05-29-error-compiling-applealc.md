---
layout: post
title: "编译AppleALC出现错误"
date: 2022-05-29 07:01:10 +08:00
categories: ["笔记"]
---

> In subcomponent: /Users/admin/Library/Developer/Xcode/DerivedData/AppleALC-fqueikknxpxowubueomyyxuwlnmg/Build/Products/Debug/AppleALC.kext/Contents/PlugIns/PinConfigs.kext/Contents/Info.plist.md5 Command CodeSign failed with a nonzero exit code

解决办法

`Other Code Signing Flags`添加参数`--deep`