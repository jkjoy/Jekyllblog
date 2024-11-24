---
layout: post
title: "解决apt-get安装中的E: Sub-process /usr/bin/dpkg returned an error code (1)问题"
date: 2023-05-10 13:20:18 +08:00
categories: ["笔记"]
tags: ["linux"]
---
在用apt-get安装软件包的时候遇到E: Sub-process /usr/bin/dpkg returned an error code (1)问题，解决方法如下： \# 现将info文件夹更名

```
cd /var/lib/dpkg/sudo 
```

```
mv info/ info_bak 
```

  \# 再新建一个新的info文件夹

```
sudo mkdir info
```

\# 更新

```
sudo apt-get update
```

\# 修复

```
sudo apt-get -f install
```

\# 执行完上一步操作后会在新的info文件夹下生成一些文件，现将这些文件全部移到info\_bak文件夹下

```
sudo mv info/* info_bak/
```

  # 把自己新建的info文件夹删掉

```
sudo rm -rf info
```

\# 把以前的info文件夹重新改回名

```
sudo mv info_bak info
```