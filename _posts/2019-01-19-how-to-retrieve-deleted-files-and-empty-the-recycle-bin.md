---
layout: post
title: "怎么找回已被删除并清空回收站的文件"
date: 2019-01-19 01:15:49 +08:00
categories: ["笔记"]
---

<p>如果你遇到过一不小心把文件删错了，还把回收站清空了，咋办啊？
只要三步，你就能找回你删掉并清空回收站的东西</p>
<p>步骤：</p>
<p>1、单击“开始——运行，然后输入regedit （打开注册表）</p>
<p>2、依次展开：HEKEY——LOCAL——MACHIME/SOFTWARE/microsoft/WINDOWS/ CURRENTVERSION/EXPLORER/DESKTOP/NAMESPACE 在左边空白外点击“新建”</p>
<p>，选择：“主键”，把它命名为“645FFO40——5081——101B——9F08——00AA002F954E”</p>
<p>再把右边的“默认”的主键的键值设为“回收站”，然后退出注册表。就OK啦。</p>
<p>3、要重启计算机。</p>
<p>只要机器没有运行过磁盘整理。系统完好.任何时候的文件都可以找回来。</p>