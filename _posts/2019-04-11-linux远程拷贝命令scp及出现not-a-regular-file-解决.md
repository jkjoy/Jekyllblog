---
layout: post
title: "linux远程拷贝命令scp及出现not a regular file 解决"
date: 2019-04-11 09:16:58 +08:00
categories: ["默认"]
---

<p>最近开始折腾ubuntu使用命令行上传下载还是挺方便的。
想备份数据到本地
那就使用scp命令
scp提供了几个选项  在scp后加就行了</p>
<blockquote>
<pre><code>-p 拷贝文件的时候保留源文件建立的时间。
-q 执行文件拷贝时，不显示任何提示消息。
-r 拷贝整个目录
-v 拷贝文件时，显示提示信息。
</code></pre>
</blockquote>
<p>将远程主机192.168.1.23的/home/adm/目录下所有文件下载至本地/home/sun，则命令为：</p>
<blockquote>
  scp -r root@192.168.1.23:/home/adm/  /home/sun/
</blockquote>
<p>回车后输入密码就可以了</p>
<p>ps
linux 下scp传文件时错误 scp: /usr/tools: not a regular file 不能成功传送
1：有可能没权限 chmod 777
2:  在使用scp时加上-r 参数</p>