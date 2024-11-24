---
layout: post
title: "解决：gitalk 报错 Error: Validation Failed.--MD5 加密 id 避免 github issue lables 50 字符限制"
date: 2023-03-21 14:42:06 +08:00
categories: ["笔记"]
---

<p>解决：gitalk 报错 Error: Validation Failed.--MD5 加密 id 避免 github issue lables 50 字符限制
创建一个<code>github gist</code> 文件保存</p>
<pre><code>https://github.com/blueimp/JavaScript-MD5/blob/master/js/md5.min.js</code></pre>
<p>js 源码：</p>
<pre><code>https://gist.githubusercontent.com/qhh0205/78e9e0b1f3114db6737f3ed8cdd51d3a/raw/3894c5be5aa2378336b1f5ee0f296fa0b22d06e9/md5.min.js</code></pre>
<p>将 gist 链接嵌入到 <code>layout/_third-party/comments/gitalk.swig </code>文件，嵌入时的 js 链接地址需要注意下：</p>
<p>不能直接写第一步的创建的 gitst 链接地址，需要将 <code>gist.githubusercontent.com</code> 替换为 <code>rawgit.com</code>。即嵌入地址为:</p>
<pre><code>https://rawgit.com/qhh0205/78e9e0b1f3114db6737f3ed8cdd51d3a/raw/3894c5be5aa2378336b1f5ee0f296fa0b22d06e9/md5.min.js</code></pre>
<p>最终 <code>layout/_third-party/comments/gitalk.swig</code> 配置如下：</p>
<pre><code class="language-JS">{% if page.comments &amp;&amp; theme.gitalk.enable %}
  &lt;link rel=&quot;stylesheet&quot; href=&quot;https://unpkg.com/gitalk/dist/gitalk.css&quot;&gt;
  &lt;script src=&quot;https://unpkg.com/gitalk/dist/gitalk.min.js&quot;&gt;&lt;/script&gt;
  &lt;script src=&quot;https://rawgit.com/qhh0205/78e9e0b1f3114db6737f3ed8cdd51d3a/raw/3894c5be5aa2378336b1f5ee0f296fa0b22d06e9/md5.min.js&quot;&gt;&lt;/script&gt;
   &lt;script type=&quot;text/javascript&quot;&gt;
        var gitalk = new Gitalk({
          clientID: &#039;3840ba8c8d80c18be7e3&#039;,
          clientSecret: &#039;1b00f2efe5285973c24da9ed9ac895775eacc8ea&#039;,
          repo: &#039;{{ theme.gitalk.repo }}&#039;,
          owner: &#039;{{ theme.gitalk.githubID }}&#039;,
          admin: [&#039;{{ theme.gitalk.adminUser }}&#039;],
          id: md5(location.pathname),
          distractionFreeMode: &#039;{{ theme.gitalk.distractionFreeMode }}&#039;
        })
        gitalk.render(&#039;gitalk-container&#039;)
    &lt;/script&gt;
{% endif %}</code></pre>