---
layout: post
title: "无插件实现sitemap XML版"
date: 2018-05-19 13:11:22 +08:00
categories: ["默认"]
---

无插件实现sitemap XML版代码如下，新建xmlmap.php文件在wordpress根目录

```php
<?php
require('./wp-blog-header.php');
header("Content-type: text/xml");
header('HTTP/1.1 200 OK');
$posts_to_show = 1000; // 获取文章数量
echo '<?xml version="1.0" encoding="UTF-8"?>';
echo '<urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">';
?>
<!-- generated-on=<?php echo get_lastpostdate('blog'); ?>-->
<?php
header("Content-type: text/xml");
$myposts = get_posts( "numberposts=" . $posts_to_show );
foreach( $myposts as $post ) { ?>
 <url>
 <loc><?php the_permalink(); ?></loc>
 <lastmod><?php the_time('c') ?></lastmod>
 <changefreq>monthly</changefreq>
 <priority>0.6</priority>
 </url>
<?php } // end foreach ?>
</urlset>
```

重写规则如下

```HTML
rewrite ^/sitemap.xml$ /xmlmap.php;
rewrite ^/sitemap_baidu.xml$ /xmlmap_sp.php;
```