---
layout: post
title: "Xcode 编译applealc出现签名错误的解决方法"
date: 2021-11-01 18:08:00 +08:00
categories: ["默认"]
---

<h2>报错如下</h2><blockquote>In subcomponent:<br />/Users/admin/Library/Developer/Xcode/DerivedData/AppleALC-fqueikknxpxowubueomyyxuwlnmg/Build/Products/Debug<br />/AppleALC.kext/Contents/PlugIns/PinConfigs.kext/Contents/Info.plist.md5<br />Command CodeSign failed with a nonzero exit code</blockquote><h2>解决方法</h2><p>在Other Code Signing Flags添加参数--deep</p>