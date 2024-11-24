---
layout: post
title: " The system cannot communicate with the DNS server and returns the error."
date: 2023-05-09 15:48:21 +08:00
categories: ["吐槽"]
---

## 出现问题
ping baidu.com出现报错,原因是DNS错误
![output-from-ping-phoenixnap-com-temporary-failure-in-name-resolution.png][1]
## 解决办法
修改DNS为8.8.8.8即可
```
sudo nano /etc/resolv.conf
```

  [1]: https://blogcdn.asbid.cn/2023/05/09/1683618372.png