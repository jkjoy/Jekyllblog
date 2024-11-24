---
layout: post
title: "wordpress归档页面"
date: 2018-06-13 23:17:26 +08:00
categories: ["默认"]
---

<p>如果已有archives.php文件，我们直接打开修改其中内容即可，将一下代码复制进去：</p>
<pre><code class="language-php">&lt;div class=archives&gt;
&lt;?php
$previous_year = $year = 0;
$previous_month = $month = 0;
$ul_open = false;
$myposts = get_posts(&#039;numberposts=-1&amp;orderby=post_date&amp;order=DESC&#039;);
foreach($myposts as $post) :
setup_postdata($post);
$year = mysql2date(&#039;Y&#039;, $post-&gt;post_date);
$month = mysql2date(&#039;n&#039;, $post-&gt;post_date);
$day = mysql2date(&#039;j&#039;, $post-&gt;post_date);
if($year != $previous_year || $month != $previous_month) :
if($ul_open == true) :
echo &#039;&lt;/ul&gt;&#039;;
endif;
echo &#039;&lt;h4 class=m-title&gt;&#039;; echo the_time(&#039;Y-m&#039;); echo &#039;&lt;/h4&gt;&#039;;
echo &#039;&lt;ul class=archives-monthlisting&gt;&#039;;
$ul_open = true;
endif;
$previous_year = $year; $previous_month = $month;
?&gt;
&lt;li&gt;
&lt;a href=&lt;?php the_permalink(); ?&gt;&gt;&lt;span&gt;&lt;?php the_time(&#039;Y-m-j&#039;); ?&gt;&lt;/span&gt;
&lt;div class=atitle&gt;&lt;?php the_title(); ?&gt;&lt;/div&gt;&lt;/a&gt;
&lt;/li&gt;
&lt;?php endforeach; ?&gt;
&lt;/ul&gt;
&lt;/div&gt;
</code></pre>
<p>不是全部复制哦，相信大家可以在archives.php文件中找到和以上代码一样以： 开头和 </p>
<p>结尾的部分，替换这一部分即可。 剩下的就是加入css样式了，在style.css中加入下列代码即可，（dux或特别主题只需在后台自定义css样式中加入即可） </p>
<pre><code class="language-css">.archive-title{border-bottom:1px #eee solid;position:relative;padding-bottom:4px;margin-bottom:10px}
.archives li a{padding:8px 0;display:block}
.archives li a:hover .atitle:after{background:#428bca}
.archives li a span{display:inline-block;width:100px;font-size:12px;text-indent:20px}
.archives li a .atitle{display:inline-block;padding:0 15px;position:relative}
.archives li a .atitle:after{position:absolute;left:-6px;background:#ccc;height:8px;width:8px;border-radius:6px;top:6px;content:}
.archives li a .atitle:before{position:absolute;left:-4px;background:#fff;height:12px;width:12px;border-radius:6px;top:6px;content:}
.archives{position:relative;padding:10px 0}
.archives:before{height:95%;width:4px;background:#e6e6e6;position:absolute;left:100px;content:;top:30px}
.m-title{position:relative;margin:10px 0;cursor:pointer}
.m-title:hover:after{background:#ff5c43}
.m-title:before{position:absolute;left:94px;background:#fff;height:16px;width:16px;border-radius:8px;top:8px;content:}
.m-title:after{position:absolute;left:96px;background:#ccc;height:12px;width:12px;border-radius:6px;top:10px;content:}
</code></pre>