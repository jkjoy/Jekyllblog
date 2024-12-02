---
layout: post
title: "CentOS一键安装ShadowsocksR服务(附单/多端口管理)"
date: 2019-04-04 03:02:00 +08:00
categories: ["分享"]
---

<pre><code class="lang-bash">wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh &amp;&amp; chmod +x ssr.sh &amp;&amp; bash ssr.sh</code></pre><p>使用wget命令下载文件，-N代表不重新下载文件除非比本地文件更新，--no-check-certificate代表不检查证书。</p><p>下载完成后可以看到以下界面，按提示操作输入端口/密码/加密方式/ 协议/混淆等参数即可完成安装。<br /><img src="https://xy07-1251893119.costj.myqcloud.com/2019/04/03/4001117836.png" alt="20190211153929924.png" title="20190211153929924.png"><br />安装完成后，如需要进入服务界面输入以下命令。</p><pre><code>bash ssr.sh</code></pre><p>安装完成后，自动设置为系统服务，所以支持使用服务来启动/停止等操作，同时支持开机启动。</p><blockquote>service ssr start    //启动 <br />service ssr stop    //停止  <br />service ssr restart //重启 <br />service ssr status</blockquote><p>ShadowsocksR 默认支持UDP转发，服务端无需任何设置。</p><p>本脚本已经集成了 安装/卸载 锐速(ServerSpeeder)，但是是否支持请查看 Linux支持内核列表 。</p>