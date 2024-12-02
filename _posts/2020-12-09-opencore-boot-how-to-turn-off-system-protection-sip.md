---
layout: post
title: "OpenCore引导如何关闭系统保护sip"
date: 2020-12-09 15:29:00 +08:00
categories: ["分享"]
---

<p>OpenCore 关闭系统保护方法；</p><p>NVRAM — 7C436110-AB2A-4BBB-A880-FE41995C9F82 — csr-active-config 填入DATA值：</p><pre><code>E7030000
</code></pre><p>如果安装出现进入安装界面空白 则需要开启SIP。</p>