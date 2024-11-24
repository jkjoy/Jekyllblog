---
layout: post
title: "自动同步Mastodon到Memos"
date: 2024-01-13 19:02:00 +08:00
categories: ["分享"]
tags: ["mastodon", "memos"]
---

## 前言

为了更加方便的同步内容,可以作备份之用.

## 声明

代码和功能实现来自于[@大大的蜗牛](https://e5n.cc/@eallion "@大大的蜗牛") 原理是使用webhook. 在发布内容时,触发脚本运行.

## 步骤

### 同步脚本

脚本中`API_HOST`为memos的API `AUTHORIZATION`为memos中Token `CONTENT_URL`中`111363033003475492`为mastodon的用户的ID 获得用户ID的方法可以参见 

[article id="1469"]

```bash
#!/bin/sh

# API 和 Token
API_HOST="https://memos.ee/api/v1/memo"
AUTHORIZATION="Bearer eyJhbGciOiJIUzI1NiIsImtpZCI6InYxIiwidHlwIjoiSldUIn0.eyJuYW1lIjoiamtqb3kiLCJpc3MiOiJtZW1vcyIsInN1YiI6IjEiLCJhdWQiOlsidXNlci5hY2Nlc3MtdG9rZW4iXSwiaWF0IjoxNjk3ODc0NTk2fQ.jNGMDE1YVX4Qj6hNhmrxb63WlRM5kGX10k_qRXH6ID4"

# 原始内容
CONTENT_URL="https://09j.cn/api/v1/accounts/111363033003475492/statuses?limit=1"
CONTENT=$(curl --connect-timeout 60 -s $CONTENT_URL | jq -r &#039;.[0]&#039;)
# mastodon
MASTODON_URL=$(echo $CONTENT | grep -oP &#039;https:\/\/09j\.cn\/@[^\/]+\/\d+&#039;)
DUDU_CONTENT="[自动转发自我的Mastodon]($MASTODON_URL)"

MENTIONS=$(echo $CONTENT | jq -r &#039;.mentions[]&#039;)
if [ ! -z "$MENTIONS" ]; then
  echo "Skipping status mention! $(TZ=UTC-8 date +"%Y-%m-%d"" ""%T")"
  echo ======================================================
  exit 0
fi

MEDIA=$(echo $CONTENT | jq -r &#039;.media_attachments&#039;)
# 判断 Media 的内容
if [ "$MEDIA" != "null" ]; then
  MEDIAS=$(echo $CONTENT | jq -r &#039;.media_attachments[] | select(.type=="image") | .url&#039;)
  # 拼接图片
  images=""
  for url in $MEDIAS; do
    images="$images![image]($url)\n"
  done
  TEXT=$(echo "$CONTENT" | jq -r &#039;.content&#039; | sed &#039;s/ +/ /g&#039; | lynx -dump -stdin -nonumbers -nolist | tr -d &#039;\n&#039; | sed &#039;/^$/N;s/\n\n/\n/g&#039; | sed &#039;s/^[[:space:]]*//;s/[[:space:]]*$//&#039;)
  TEXT="$TEXT\n$DUDU_CONTENT"
  TEXT="$TEXT\n$images"

else
   # 普通内容
  TEXT=$(echo "$CONTENT" | jq -r &#039;.content&#039; | sed &#039;s/ +/ /g&#039; | lynx -dump -stdin -nonumbers -nolist | tr -d &#039;\n&#039; | sed &#039;/^$/N;s/\n\n/\n/g&#039; | sed &#039;s/^[[:space:]]*//;s/[[:space:]]*$//&#039;)
  TEXT="${TEXT}\n$DUDU_CONTENT"
fi

curl -X POST \
  -H "Accept: application/json" \
  -H "Authorization: $AUTHORIZATION" \
  -d "{ \"content\": \"$TEXT\" }" \
  $API_HOST

echo Sync Mastodon to Memos Successful! $(TZ=UTC-8 date +"%Y-%m-%d"" ""%T")
echo ======================================================
```

我稍微做了一点修改.在发布到memos的同时贴上原本mastodon的原文链接. 由于我不会写规则,就随意写了匹配规则 我的实例为09j.cn 不需要则删除以下

```bash
MASTODON_URL=$(echo $CONTENT | grep -oP &#039;https:\/\/09j\.cn\/@[^\/]+\/\d+&#039;)
DUDU_CONTENT="[自动转发自我的Mastodon]($MASTODON_URL)" 
```

```sh
TEXT="$TEXT\n$DUDU_CONTENT"
```

即可

### 部署webhook

Docker镜像是根据官方dockerfile增加了中文支持,

推荐使用docker-compose部署 编辑`docker-compose.yaml`内容为

```yaml
services:
  webhook:
    image: jkjoy/webhook
    container_name: webhook
    command: -verbose -hooks=hooks.yml -hotreload
    environment:
      - TZ=Asia/Chongqing #中国时区
      - LANG=C.UTF-8  #中文支持
    volumes:
      - ./config:/config:ro
    ports:
      - 9000:9000
    restart: always
```

在根目录下创建`config`目录,并在`config`下创建`hooks.yml`文件并编辑内容为

```yaml
- id: memos
  execute-command: "/config/memos.sh"
  command-working-directory: "/"
```

把脚本内容保存为`memos.sh`保存在`config`目录下

然后在`docker-compose.yaml`所在的根目录下 运行`docker compose up -d`即可

## 使用Webhook

`hooks.yaml`为webhook的配置

其中的`execute-command`为可执行脚本

webhook的访问地址格式为

```sh
服务器 ip:端口/hooks/ID
```

以127.0.0.1为例 访问http://127.0.0.1:9000/hooks/memos

## 设置mastodon

在管理员后台中`管理`\-`webhooks`\-`新增对端` 对端URL填入http://127.0.0.1:9000/hooks/memos 已启用事件选择`status.created` 点击新增即可在发布新的嘟嘟时同步内容到memos了.

## 其他

同理也可以使用webhook在发布memos时候同步到其他拥有API的服务中了.