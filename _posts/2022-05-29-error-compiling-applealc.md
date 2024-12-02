---
layout: post
title: "编译AppleALC出现错误"
date: 2022-05-29 07:01:10 +08:00
categories: ["笔记"]
---

<blockquote>
In subcomponent: /Users/admin/Library/Developer/Xcode/DerivedData/AppleALC-fqueikknxpxowubueomyyxuwlnmg/Build/Products/Debug/AppleALC.kext/Contents/PlugIns/PinConfigs.kext/Contents/Info.plist.md5
Command CodeSign failed with a nonzero exit code
</blockquote>
<p>解决办法</p>
<p>Other Code Signing Flags添加参数--deep</p>