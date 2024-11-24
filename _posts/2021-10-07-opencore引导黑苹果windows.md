---
layout: post
title: "解决opencore引导黑苹果&amp;Windows双系统蓝屏的问题"
date: 2021-10-07 11:27:24 +08:00
categories: ["笔记"]
---

<p><del>最好的办法就是使用mod版本的opencore</del>
开机蓝屏报错的解决办法</p>
<p>打开config.plist查找<span style="color:red;"></span></p>
<p><code>booter</code>---<code>Quirks</code>---<code>SyncRuntimePermissions</code>的值改成<span style="color:red;">true</span>即可。</p>