---
layout: post
title: "ubuntu如何更改显示器分辨率并永久保存所设置的分辨率"
date: 2019-04-10 17:52:00 +08:00
categories: ["笔记"]
tags: ["命令", "xrandr", "保存", "ubuntu"]
---

终端执行命令行如下

    cvt 1920 1080
    xrandr –newmode 1920x1080_60 173.00 1920 2048 2248 2576 1080 1083 1088 1120 -hsync +vsync
    xrandr –addmode VGA-0 1920x1080_60
    xrandr –output VGA-0 –mode 1920x1080_60

然后执行
`sudo gedit .profile`
把以上的命令行复制粘贴到最后即可
保存 重启系统，使用“`xrandr`”命令查看
![2019-04-10 18-03-21 的屏幕截图.png][1]


  [1]: https://xy07-1251893119.costj.myqcloud.com/2019/04/10/465359891.png