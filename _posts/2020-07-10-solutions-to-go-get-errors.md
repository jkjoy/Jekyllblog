---
layout: post
title: "go get出现错误的解决办法"
date: 2020-07-10 21:31:08 +08:00
categories: ["分享"]
---

<p>错误提示<br />unrecognized import path "golang.org/x/sys/windows": https fetch: Get "https://golang.org/x/sys/windows?go-get=1": dial tcp 216.239.37.1:443: connectex: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.<br />解决办法</p><p>mkdir -p $GOPATH/src/golang.org/x<br />cd $GOPATH/src/golang.org/x<br />git clone <a href="https://github.com/golang/sync.git">https://github.com/golang/sync.git</a><br />git clone <a href="https://github.com/golang/crypto.git">https://github.com/golang/crypto.git</a><br />git clone <a href="https://github.com/golang/sys.git">https://github.com/golang/sys.git</a><br />————————————————</p><p>原文链接：<a href="https://blog.csdn.net/cyLee_/java/article/details/93159032">https://blog.csdn.net/cyLee_/java/article/details/93159032</a></p>