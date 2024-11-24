---
layout: post
title: "给wordpress的链接添加nofollow选项的方法"
date: 2017-01-24 20:53:05 +08:00
categories: ["默认"]
---

<p>擅自给网站友情链接添加上nofollow属性是个极其不道德的行为。但是，有时候我们的友链网站被搜索引擎惩罚，为了避免被其连累，先通知对方，给其链接添上“nofollow”属性，等网站恢复后再取消，也是必要的。然而，一般而言，网站的友链都是通过后台调用的，后台的XFN关系是没有nofollow选项的。这里提供一个方法，通过修改wp-admin/includes/meta-boxes.php,在后台XFN关系处添加上nofollow选项,效果如下图</p>
<p>打开meta-boxes.php，通过Ctrl+F找到function link_xfn_meta_box($link)，我们发现，控制友情关系的一段代码有着极高的相似性，见下面代码：</p>
<blockquote>&lt;label for="contact"&gt;
&lt;input id="contact" class="valinp" name="friendship" type="radio" value="contact" /&gt; /&amp;gt; &lt;!--?php /* translators: xfn: http://gmpg.org/xfn/ */ _e('contact') ?--&gt;
&lt;/label&gt;
&lt;label for="acquaintance"&gt;
&lt;input id="acquaintance" class="valinp" name="friendship" type="radio" value="acquaintance" /&gt; /&amp;gt; &lt;!--?php /* translators: xfn: http://gmpg.org/xfn/ */ _e('acquaintance') ?--&gt;
&lt;/label&gt;
&lt;label for="friend"&gt;
&lt;input id="friend" class="valinp" name="friendship" type="radio" value="friend" /&gt; /&amp;gt; &lt;!--?php /* translators: xfn: http://gmpg.org/xfn/ */ _e('friend') ?--&gt;
&lt;/label&gt;
&lt;label for="friendship"&gt;
&lt;input id="friendship" class="valinp" name="friendship" type="radio" value="" /&gt; /&amp;gt; &lt;!--?php /* translators: xfn: http://gmpg.org/xfn/ */ _e('none') ?--&gt;
&lt;/label&gt;</blockquote>
<p>这4段代码分别对应的是XFN关系的&quot;偶有联系&quot;、“熟人”“朋友”和“无&quot;。
依葫芦画瓢，直接在对应“无”的代码下面，添上如下代码，就能成功添上nofollow选项。</p>
<blockquote>&lt;label for="nofollow"&gt;
&lt;input id="nofollow" class="valinp" name="friendship" type="radio" value="nofollow" /&gt; /&amp;gt; &lt;!--?php /* translators: xfn: http://gmpg.org/xfn/ */ _e('nofollow') ?--&gt;
&lt;/label&gt;</blockquote>
<p>效果如下图：</p>
<p>同样的道理，如果想把nofollow添加在其他位置，比如职场关系、地理关系、家庭关系等，只需要找到其对应的代码，按着上面的方法，简单的“复制-修改”一下，添加在代码下面即可。如下图：</p>
<p>经过这么修改，以后我们要给一个友情链接添加上nofollow就十分方便了，而且添加后，在后台设置-链接表首页，也会有nofollow的关系提示，要找到带有nofollow属性的超链接也会十分快捷。</p>