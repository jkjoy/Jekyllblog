---
layout: post
title: "无插件实现sitemap XML版"
date: 2018-05-19 13:11:22 +08:00
categories: ["默认"]
---

<p>无插件实现sitemap XML版代码如下，新建xmlmap.php文件在wordpress根目录</p>
<pre><code class="language-php  line-numbers">&lt;?php
require('./wp-blog-header.php');
header("Content-type: text/xml");
header('HTTP/1.1 200 OK');
$posts_to_show = 1000; // 获取文章数量
echo '&lt;?xml version="1.0" encoding="UTF-8"?&gt;';
echo '&lt;urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"
xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"&gt;';
?&gt;
&lt;!-- generated-on=&lt;?php echo get_lastpostdate('blog'); ?&gt;--&gt;
&lt;?php
header("Content-type: text/xml");
$myposts = get_posts( "numberposts=" . $posts_to_show );
foreach( $myposts as $post ) { ?&gt;
 &lt;url&gt;
 &lt;loc&gt;&lt;?php the_permalink(); ?&gt;&lt;/loc&gt;
 &lt;lastmod&gt;&lt;?php the_time('c') ?&gt;&lt;/lastmod&gt;
 &lt;changefreq&gt;monthly&lt;/changefreq&gt;
 &lt;priority&gt;0.6&lt;/priority&gt;
 &lt;/url&gt;
&lt;?php } // end foreach ?&gt;
&lt;/urlset&gt;
</code></pre>
<p>重写规则如下</p>
<pre data-language=HTML><code class="language-markup  line-numbers">rewrite ^/sitemap.xml$ /xmlmap.php;
rewrite ^/sitemap_baidu.xml$ /xmlmap_sp.php;
</code></pre>