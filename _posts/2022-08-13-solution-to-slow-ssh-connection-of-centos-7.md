---
layout: post
title: "centos7 ssh连接慢的解决方法"
date: 2022-08-13 00:52:00 +08:00
categories: ["默认"]
tags: ["SSH"]
---

<pre><code class="lang-bash">vim /etc/ssh/sshd_config</code></pre><p>按i编辑插入<br />找到<br /><code>UseDNS</code>去掉前面的#号 改为 no</p><p><code>GSSAPIAuthentication</code> 改为 no</p><p>然后<code>：wq </code>保存退出</p><pre><code class="lang-bash">systemctl restart sshd</code></pre><p>重启</p>