---
layout: post
title: "一键部署X-UI面板"
date: 2018-10-19 12:47:00 +08:00
categories: ["分享"]
tags: ["部署"]
---

### 功能介绍
- 系统状态监控
- 支持多用户多协议，网页可视化操作
- 支持的协议：vmess、vless、trojan、shadowsocks、dokodemo-door、socks、http
- 支持配置更多传输配置
- 流量统计，限制流量，限制到期时间
- 可自定义 xray 配置模板
- 支持 https 访问面板（自备域名 + ssl 证书）
- 支持一键SSL证书申请且自动续签
- 更多高级配置项，详见面板

### 安装&升级

```BASH
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

### 项目地址
https://github.com/vaxilu/x-ui

### 适合国内环境
 [install.zip][1]
或执行
```sh
bash <(curl -Ls https://down.asbid.cn/x-ui/install.sh)
```


  [1]: https://blogcdn.asbid.cn/2023/07/27/1690426036.zip