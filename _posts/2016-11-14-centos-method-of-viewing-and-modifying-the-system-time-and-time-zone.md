---
layout: post
title: "CentOS系统时间和时区查看以及修改的方法"
date: 2016-11-14 13:38:48 +08:00
categories: ["默认"]
---

<p>一、时间修改</p>
<p>远程连接到centos 或者直接登录系统</p>
<h1>date 查看系统时间</h1>
<h1>date -s 修改时间</h1>
<p>看下面的例子</p>
<h1>date -s  03/04/2013（将系统日期设定为2013年03月04日）</h1>
<h1>date -s  110:38（将系统时间设定为上午 10:38）</h1>
<p>二、时区修改</p>
<p>先查看时区</p>
<p>date -R</p>
<p>&nbsp;</p>
<p>修改时区：</p>
<p>（将Asia/shanghai-上海时区写入当前时区）</p>
<h1>cp -f /usr/share/zoneinfo/Asia/Shanghai     /etc/localtime</h1>
<p>提示是否覆盖,输入Y回车,</p>
<p>然后</p>
<h1>date</h1>
<p>查看时区和时间（CST,中国时区）</p>