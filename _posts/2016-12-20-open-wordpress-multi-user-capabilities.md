---
layout: post
title: "开启wordpress多用户功能"
date: 2016-12-20 13:48:31 +08:00
categories: ["默认"]
---

编辑根目录的 wp-config.php 文件，找到以下代码：
```php
 define ('WPLANG', 'zh\_CN');
```
在其之后添加以下代码：
```php
define('WP\_ALLOW\_MULTISITE', true);
```
这个时候刷新后台页面，工具菜单中已经有添加网络 (Network) 选项。