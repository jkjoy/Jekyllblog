---
layout: post
title: "利用QQ机器人在有WordPress评论时QQ消息通知"
date: 2024-03-05 18:50:00 +08:00
categories: ["分享"]
tags: ["wordpress"]
---

## 项目

![icon](https://imsun.oss-cn-shanghai.aliyuncs.com/2024/03/1710062614-cc35d4b8e796c869289176c383aa3da3.png) 

https://github.com/Mrs4s/go-cqhttp

## 效果

![](https://imsun.oss-cn-shanghai.aliyuncs.com/2024/03/1710061520-99e44cb313033ccf463cafbc1218ef06.png)

## 使用

在主题文件夹中的`function.php`添加以下代码

> 代码中有部分无法正确渲染的内容请查看置顶评论

```php
function bot_msg_qq($comment_id)
{
    $comment = get_comment($comment_id);
//如果评论作者是管理员，直接返回不处理
    if( user_can($comment->user_id, 'administrator') )
    {
        return;
    }
    $siteurl = get_bloginfo('url');
    $text = '文章《' . get_the_title($comment->comment_post_ID) . '》有新的评论！';
    $desp = $text . "\n" . "作者: $comment->comment_author \n邮箱: $comment->comment_author_email \n评论: $comment->comment_content \n点击查看：$siteurl/?p=$comment->comment_post_ID#comments";
    // 封装Object，message是我们需要推送到 QQ 的消息内容
    $postdata = http_build_query(
        array(
            'message' => $desp
        )
    );
    // 执行POST请求
    $opts = array('http' =>
        array(
            'method' => 'POST',
            'header' => 'Content-type: application/x-www-form-urlencoded',
            'content' => $postdata
        )
    );
    $context = stream_context_create($opts);  
    return $result = file_get_contents('https://bot.asbid.cn/send_private_msg?user_id=接收qq号', false, $context);
}
add_action('comment_post', 'bot_msg_qq', 19, 2);
```

* 修改QQ机器人的`API`或者保持默认
* 修改接收通知的QQ号码
* `QQ机器人`与接收通知的`QQ号码`必须为好友

> 我的QQ机器人号码 `2280858259` 
API: [https://bot.asbid.cn](https://bot.asbid.cn) 
务必添加QQ`2280858259`为好友,不然无法接收消息

## 相关插件
 https://www.imsun.org/archives/346.html

## 引用

https://www.boxmoe.com/534.html

