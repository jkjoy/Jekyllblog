---
layout: post
title: "解决apt-get安装中的E: Sub-process /usr/bin/dpkg returned an error code (1)问题"
date: 2023-05-10 13:20:18 +08:00
categories: ["笔记"]
tags: ["linux"]
---

在用apt-get安装软件包的时候遇到E: Sub-process /usr/bin/dpkg returned an error code (1)问题，解决方法如下：

# 现将info文件夹更名
<pre class="corepress-code-pre"><code>cd /var/lib/dpkg/sudo </code></pre>
<pre class="corepress-code-pre"><code>mv info/ info_bak </code></pre>
&nbsp;

# 再新建一个新的info文件夹
<pre class="corepress-code-pre"><code>sudo mkdir info</code></pre>
# 更新
<pre class="corepress-code-pre"><code>sudo apt-get update</code></pre>
# 修复
<pre class="corepress-code-pre"><code>sudo apt-get -f install</code></pre>
# 执行完上一步操作后会在新的info文件夹下生成一些文件，现将这些文件全部移到info_bak文件夹下
<pre class="corepress-code-pre"><code>sudo mv info/* info_bak/</code></pre>
&nbsp;

# 把自己新建的info文件夹删掉
<pre class="corepress-code-pre"><code>sudo rm -rf info</code></pre>
# 把以前的info文件夹重新改回名
<pre class="corepress-code-pre"><code>sudo mv info_bak info</code></pre>
&nbsp;