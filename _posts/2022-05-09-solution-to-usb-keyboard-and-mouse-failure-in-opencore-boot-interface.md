---
layout: post
title: "opencore引导界面USB键盘鼠标失效的解决办法"
date: 2022-05-09 18:32:00 +08:00
categories: ["测试"]
---

无法在选择器中选择任何内容这是由于某些原因不兼容的键盘驱动程序：

config.plist中禁用PollAppleHotKeys并启用KeySupport，然后从您的config.plist->UEFI->Drivers 子项删除OpenUsbKbDxe驱动

如果上述方法无效，请反向操作：在config.plist中禁用 KeySupport，然后把OpenUsbKbDxe 驱动添加到您的config.plist-> UEFI->Drivers  下面

