---
layout: post
title: "ubuntu  无线/Wifi 上网速度慢的解决方法"
date: 2019-04-10 15:20:43 +08:00
categories: ["笔记"]
---

<p>装了Ubuntu 后连接无线上网，发现出奇的慢。网上查找亲测有效的方法为：
1、在终端运行：sudo gedit /etc/modprobe.d/iwlwifi.conf
2、在打开的这个配置文件中空白处添加：options iwlwifi 11n_disable=1
3、保存文件并重启。（本人已成功）</p>
<p>对比win7下速度差不多了</p>