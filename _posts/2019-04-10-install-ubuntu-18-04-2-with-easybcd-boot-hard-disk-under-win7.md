---
layout: post
title: "win7下用easyBCD引导硬盘安装ubuntu-18.04.2"
date: 2019-04-10 10:50:48 +08:00
categories: ["笔记"]
---

Win7装Ubuntu双系统，不需要U盘 本文测试安装的是64位ubuntu-18.04.2

#### 准备

+   win7系统
+   ubuntu系统镜像文件
+   easyBCD

#### Step 1.划分硬盘

计算机右键，管理，磁盘管理，通过压缩卷等方法得到要分给 Ubuntu系统的分区。或者原来你就有某个盘用于装 Ubuntu。 将该卷删除。

![](https://mrwen.oss-cn-shanghai.aliyuncs.com/2019/04/1.jpg) 
![](https://mrwen.oss-cn-shanghai.aliyuncs.com/2019/04/2.jpg)

在磁盘管理里将C盘执行压缩卷，然后把压缩后的空闲空间格式化成FAT32类型。 压缩后的5G空间盘符变成F盘 需要将ubuntu-18.04.2-desktop-amd64.iso和镜像文件casper文件夹里的vmlinuz 、initrd都移到F盘。

![](https://mrwen.oss-cn-shanghai.aliyuncs.com/2019/04/3.png) 
![](https://mrwen.oss-cn-shanghai.aliyuncs.com/2019/04/4.png)

#### Step 2.使用EasyBCD引导Ubuntu ISO启动

打开EasyBCD，添加新条目，NeoGrub，安装。然后点击，配置。在出现的menu.lst最后输入一下内容：

> title Install ubuntu-18.04.2 root (hd0,1) kernel (hd0,1)/vmlinuz boot=casper iso-scan/filename=/ubuntu-18.04.2-desktop-amd64.iso ro quiet splash  locale=zh\_CN.UTF-8 initrd (hd0,1)/initrd

如果没有弹出txt文本框，则可以在C:\\NST下寻找menu.lst用记事本打开

#### Step 3.重启。选择 NeoGrub。

在安装之前打开终端（Ctrl+Alt+T），输入 
```bash
sudo umount –l /isodevice
```
注意空格，可多执行一次，以确保将挂载的镜像移除，否则将无法进行安装

![](https://mrwen.oss-cn-shanghai.aliyuncs.com/2019/04/8.png)

##### 第1步

双击桌面“安装Ubuntu”图标，稍等出来一个“欢迎”面板，检查一下左侧栏要选中了“中文(简体)”，如果不是就在左边选中它，然后点右下角“继续”按钮；

##### 第2步

是检查准备情况，要求磁盘空间足够，不要连接网络，一般不勾选更新和第三方软件，直接点“继续”按钮

##### 第3步

是询问安装到哪个分区，选择最下边的“其他选项”，点“继续”按钮

##### 第4步

接下来出来磁盘分区情况，free space 就是我们开始删除的那个卷，也就是Ubuntu要安装的硬盘。 点击选中计划要安装的分区，可以根据分区类型和大小来确定，我是 220G的空间，\\boot 2000M    swap 3G （交换空间，跟运存大小一样即可） \\home 15G  和  \\   是15G 左右 （当然，如果空间富裕，可以多分一下，/boot  2G 就可以， swap 跟随系统内存，系统内存多大就多大就好。/我分了15G，剩下空间都分给了/home。分区时候，/boot和/ 选择 ‘主分区’ ，其他选择 ‘逻辑分区’。 在出来的对话框中，设定用于分区的格式Ext4，打勾“格式化”，在“挂载点”右边点一下，选 “/”，点“确定”。注意，格式化会删除这个分区上的所有文件，请提前备份重要数据； 只有 swap 是用于“交换空间” ，其它都是 用于“Ext4”。 分区分好之后，点击确定（注意，启动引导器(grub)选择安装到 \\ 或者 \\ boot ，因为这样当Windows系统重装时，并不会影响Ubuntu系统 ）继续安装就可以了。 安装Ubuntu完毕