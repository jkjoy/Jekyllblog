---
layout: post
title: "yum提示Error: rpmdb open failed 报错处理"
date: 2022-05-25 08:53:21 +08:00
categories: ["默认"]
---

<p>宝塔面板安装docker失败时报错，可以使用以下方法重建rpm</p>
<h1>rpmdb所在目录</h1>
<pre><code class="language-bash">cd /var/lib/rpm</code></pre>
<h1>清除原rpmdb文件</h1>
<pre><code class="language-bash">rm -f __db.*</code></pre>
<h1>重建rpm数据库</h1>
<pre><code class="language-bash">rpm --rebuilddb</code></pre>
<h1>清除所有yum的缓存</h1>
<pre><code class="language-bash">yum clean all</code></pre>