---
layout: post
title: "opencore引导界面USB键盘鼠标失效的解决办法"
date: 2022-05-10 02:32:10 +08:00
categories: ["分享"]
---

<p>无法在选择器中选择任何内容这是由于某些原因不兼容的键盘驱动程序：
<code>config.plist</code>中禁用<code>PollAppleHotKeys</code>
并启用<code>KeySupport</code>，然后从您的<code>config.plist</code>-&gt;<code>UEFI</code>-&gt;<code>Drivers</code> 子项删除
<code>OpenUsbKbDxe</code>驱动
如果上述方法无效，请反向操作：在<code>config.plist</code>中禁用 <code>KeySupport</code>，然后把<code>OpenUsbKbDxe</code> 驱动添加到您的<code>config.plist</code>-&gt; <code>UEFI</code>-&gt;<code>Drivers</code> 下面</p>