---
layout: post
title: "centos7 ssh连接慢的解决方法"
date: 2022-12-02 13:40:50 +08:00
categories: ["测试"]
---

```bash
vim /etc/ssh/sshd_config
```
按i编辑插入
找到
`UseDNS`去掉前面的#号 改为 no

`GSSAPIAuthentication` 改为 no

然后`：wq `保存退出

```bash
systemctl restart sshd
```
重启