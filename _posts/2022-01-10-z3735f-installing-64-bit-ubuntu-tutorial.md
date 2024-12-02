---
layout: post
title: "z3735f安装64位的ubuntu教程"
date: 2022-01-10 21:07:55 +08:00
categories: ["默认"]
---

从海鲜市场淘了一块z3735f的mini itx主板，比thin itx主板还小一半，花了78元大洋拿下。
拥有双核心四线程，2g lpddr3l ,32g emmc硬盘，还有一个sd卡插槽，可拓展usb2.0。
由于cpu是32位，奇葩的是uefi引导只支持32位，也就是bootia32.只能通过winpe安装x86的win8及其以上版本，win7安装没有成功。
用来做小主机性能太低，做下载机没有sata接口甚至还不如路由器。
于是就想拿来做个网站服务器吧。低功耗，无风扇，应该很适合，说干就干。
用ventoy 来引导Ubuntu镜像
成功安装。但是却启动不了，这是因为主板不支持64位的GRUB引导程序，故而导致Ubuntu系统引导失败，而官网的Ubuntu系统只有64位支持UEFI引导。除了WIFI、蓝牙等驱动需要自己上网搜索安装之外，系统主要的安装和引导的具体方法如下：
<h1>一、制作安装U盘</h1>
获取IOS镜像文件，请到官网下载镜像文件<strong>请务必下载64位版本，32位只支持mbr引导不支持UEFI引导。</strong>
下载完成后下载U盘制作工具：<strong>Rufus</strong> 或 <strong>UltraISO</strong> 制作一个UEFI引导的U盘。
修改UEFI引导文件，下载 <a href="https://cdn.wyr.me/usr/uploads/2015/12/bootia32.efi_.zip">bootia32.efi</a> 文件并解压复制到’EFI\BOOT’目录下。hub
也可以在gi thub上搜索bootia32
<h1>二、安装Ubuntu操作系统</h1>
请先链接USB键鼠，使用快捷键进入BIOS（Z3735通常是DEL/ESC），修改BOOT顺序为UEFI引导的U盘。进入GRUE菜单后选择（Try Ubuntu With Install），如果之前配置的32位引导文件正确，此时你将直接进入Live CD模式的Ubuntu系统。在这个临时系统中的大部分操作都是无效的，不会被保存记录。

此时我们会看到桌面有安装Ubuntu操作系统的快捷方式，先别忙安装，看完这部分内容。点击左上角第一个应用（搜索），搜索"Disks"，进入硬盘管理软件，查看你的本地硬盘。特别提示，在平板电脑或intel stick等小型设备中，通常是SD卡模式，但绝非USB磁盘。通常显示在列表第一项。

<img class="alignnone wp-image-1419 size-full" src="https://www.imsun.org/usr/uploads/2023/12/2019110816305745-1-1.webp" alt="在这里插入图片描述" width="1275" height="630" />

<img class="alignnone wp-image-1420 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108161524441-1-1.webp" alt="在这里插入图片描述" width="1280" height="766" />由上图我们看到主硬盘所在路径为/dev/mmcblk1。由于我已经安装好了Ubuntu系统，所以看到其中有三个分区，第一个是存储EFI文件的FAT分区，第二个是存储文件的Ext4分区。如果你的平板设备还是win系统，这里应该是NTFS分区+FAT分区。这都不是重点，重点在于需要记录你的主硬盘所在路径“/dev/mmcblk1p”还是“/dev/sda1”。

记录后点击桌面的快捷方式安装ubuntu到本地硬盘。
<img class="alignnone wp-image-1421 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108161857945-1-1.webp" alt="在这里插入图片描述" width="1052" height="694" /><img class="alignnone size-full wp-image-1422" src="https://www.imsun.org/usr/uploads/2023/12/20191108161937501-1.png" alt="在这里插入图片描述" width="1136" height="817" /><img class="alignnone wp-image-1423 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162115397-1-1.webp" alt="在这里插入图片描述" width="1280" height="761" /><img class="alignnone wp-image-1424 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162305764-1-1.webp" alt="在这里插入图片描述" width="1280" height="738" /><img class="alignnone wp-image-1425 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162523782-1-1.webp" alt="在这里插入图片描述" width="1246" height="828" /><img class="alignnone wp-image-1426 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162631457-1-1.webp" alt="在这里插入图片描述" width="1121" height="742" /><img class="alignnone wp-image-1427 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162705939-1-1.webp" alt="在这里插入图片描述" width="1105" height="704" /><img class="alignnone wp-image-1428 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162718860-1-1.webp" alt="在这里插入图片描述" width="1214" height="799" /><img class="alignnone wp-image-1429 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162814769-1-1.webp" alt="在这里插入图片描述" width="1280" height="769" /><img class="alignnone wp-image-1430 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162916945-1-1.webp" alt="在这里插入图片描述" width="1127" height="470" /><img class="alignnone wp-image-1431 size-full" src="https://www.imsun.org/usr/uploads/2023/12/20191108162950489-1-1.webp" alt="在这里插入图片描述" width="972" height="486" />安装完毕进入下一步。
<h1>三、手动引导GRUB2进入本地Ubuntu操作系统</h1>
安装完毕重启我们将发现无法进入到操作系统，而是进入了EFI SHELL模式，早在意料之中，因为这类平板的CPU不支持64位的UEFI引导，但并不意味着不支持64位操作系统。

此时我们还是进入BIOS使用之前的U盘引导启动，进入GRUB菜单后不要选择，点击键盘中的"<code>c</code>"按钮，进入GRUB2命令行模式。

进入该模式后，输入“<code>ls</code>”列出硬盘分区。

此时会看到类似(hd0,gtp1)或(hd1,msdos1)之类的项。这是你的硬盘分区。其中hd0为根目录所在的磁盘，IDE硬盘用hd开始，SCSI硬盘用sd开头。软盘用fd开头。命名和linux不大一样。是从0算起。

我们需要找出linux内核所在分区。

使用"<code>ls (hdX,gtpX)/boot</code>"，其中的“X”请手动替换为上一步出现过的数字，这里肯定要有逗号","的，如果出现一大串结果，显示了你的linux内核文件，说明就是这个分区。记录X的值。

假设你在执行"<code>ls (hd0,gtp1)/boot</code>"的时候出现值，那么下一步执行：
<pre><code class="language-bash">set root=(hd0,gtp1)</code></pre>
然后输入需要输入内核路径，“<code>linux /boot/vmlinuz<em> root=/dev/mmcblk0p2</em></code>”其中号为内核版本，输入<code>/boot/vmlinuz</code>后按tab键可以进行自动补全。<code>mmcblk0p2</code>为根目录所在的分区,其中“mmcblk0”是第二步查看分区记录的值，后面的"p2"是我猜的，你顺着p1\p2\p3猜测一下，能执行就对了。完整的命令例子如下：
<pre><code class="language-bash"> linux (hd0,gpt2)/boot/vmlinuz-3.13-xxxx root=/dev/mmcblk0p5
 initrd /initrd.img
 boot</code></pre>
最后成功进入本地Ubuntu系统，这一步如果不成功的话就多尝试一下，修改上面涉及的各个值，祝你好运。
<h1>四、最后一步</h1>
到这步已经成功了一半了，但是没人愿意每次启动都使用USB的GRUB引导并手动输入引导命令，这会很麻烦。进入本地Ubuntu后，调出终端，继续输入如下命令：
<strong>执行这个代码前提条件是连接了网络，这里需要先安装好网络相关的驱动。或者用手机的usb共享网络来使用</strong>
<pre><code class="language-bash">sudo apt-get update
sudo apt-get -y purge grub-efi-amd64 grub-efi-amd64-bin grub-efi-amd64-signed
sudo apt-get -y install grub-efi-ia32-bin grub-efi-ia32 grub-common grub2-common
sudo grub-install --target=i386-efi /dev/mmcblk0p2 --efi-directory=/boot/efi/ --boot-directory=/boot/ # 这里的“mmcblk0p2 ”就是上一步你执行成功的那个值
sudo grub-mkconfig -o /boot/grub/grub.cfg</code></pre>
执行完毕后重启，发现Ubuntu引导正常，不需要USB引导也可以进入系统。恭喜！安装成功！
<blockquote>目前，我的x80HD平板能直接使用 wifi、蓝牙、屏幕触摸、屏幕旋转、声音没有解决，本人是想弄个服务器玩玩，所以声音不重要了</blockquote>