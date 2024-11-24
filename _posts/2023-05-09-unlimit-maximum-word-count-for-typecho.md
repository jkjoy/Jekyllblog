---
layout: post
title: "解除typecho的最大字数限制"
date: 2023-05-09 14:36:57 +08:00
categories: ["分享"]
tags: ["typecho"]
---

把contens表里的text字段类型设置为longtext
执行SQL
```sql
alter table typecho_contents modify text LONGTEXT
```