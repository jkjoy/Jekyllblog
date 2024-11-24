---
layout: post
title: "使用yum提示Error: rpmdb open failed的解决方案"
date: 2017-08-26 19:47:22 +08:00
categories: ["默认"]
---

<p>使用yum或者rpm安装包时出现问题，安装时报出大约如下错误</p>
<blockquote>rpmdb: Thread/process35884/139793484506880failed: Thread died inBerkeley DB library
error: db3 error(-30974) from dbenv-&gt;failchk: DB_RUNRECOVERY: Fatal error, run database recovery
error: cannot openPackages index using db3 -  (-30974)
error: cannot openPackages database in/var/lib/rpm
CRITICAL:yum.main:
Error: rpmdb openfailed</blockquote>
<p>这多半是因为rpm数据库出现损坏所致，此错误可能导致多数(甚至是所有的)rpm软件的升级、安装甚至是删除都会出现问题。</p>
<p>解决办法如下：</p>
<p>修复此错误，请以root身份在终端输入以下命令</p>
<blockquote>
   [root@www~]# cd /var/lib/rpm      # rpmdb所在目录
   [root@www rpm]# ls | grep 'db.'   # 列出相关rpmdb文件
   __db.001
   __db.002
   __db.003
   __db.004
   [root@www rpm]# for i in $(ls | grep 'db.');do mv $i $i.bak;done
   # 将原rpmdb文件都更名为结尾带.bak的文件
   或者
   [root@www rpm]# rm -f __db.*     # 清除原rpmdb文件
   [root@www rpm]# rpm --rebuilddb     # 重建rpm数据库
   [root@www rpm]# yum clean all     # 清除所有yum的缓存</blockquote>
<div>本文出自 “<a href="http://allenh.blog.51cto.com/">Craft Life</a>” 博客，请务必保留此出处<a href="http://allenh.blog.51cto.com/481430/1739188">http://allenh.blog.51cto.com/481430/1739188</a></div>