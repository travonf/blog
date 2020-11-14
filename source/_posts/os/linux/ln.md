---
title: 实际操作帮助理解Linux下的软硬链接
date: 2010-01-01 08:00:00
updated: 2010-01-01 08:00:00
tags: "linux"
categories: "OS"
---

Linux链接分两种，一种被称为硬链接用ln生成，另一种被称为软链接用ln -s生成

<!-- more -->

硬链接

硬链接指通过索引节点来进行链接。在Linux的文件系统中，保存在磁盘分区中的文件不管是什么类型都给它分配一个编号，称为索引节点号(Inode Index)。在Linux中，多个文件名指向同一索引节点是存在的。一般这种链接就是硬链接。硬链接的作用是允许一个文件拥有多个有效路径名，这样用户就可以建立硬链接到重要文件，以防止“误删”的功能。其原因如上所述，因为对应该目录的索引节点有一个以上的链接。只删除一个链接并不影响索引节点本身和其它的链接，只有当最后一个链接被删除后，文件的数据块及目录的链接才会被释放。也就是说，文件真正删除的条件是与之相关的所有硬链接文件均被删除。

ln命令可以创建硬链接：

语法格式：ln源文件 目标文件

[root@vipuser200 ~]# touch ln.txt#创建一个ln.txt文件

[root@vipuser200 ~]# echo hardlink > ln.txt #向文件中写入内容

[root@vipuser200 ~]# ln ln.txt ln2.txt#创建硬链接ln2.txt

[root@vipuser200 ~]# cat ln2.txt #查看链接文件内的内容

hardlink

[root@vipuser200 ~]# echo hardlink2 >> ln2.txt #向链接文件里面追加内容

[root@vipuser200 ~]# cat ln.txt#查看源文件

hardlink

hardlink2

编辑任意一个另外一个也随之改变

我们来查看以下这两个文件的inode号

[root@vipuser200 ~]# ll -i ln.txt ln2.txt

142337 -rw-r--r-- 2 root root 19 Jul 26 00:02 ln2.txt

142337 -rw-r--r-- 2 root root 19 Jul 26 00:02 ln.txt

注：inode号一样

我们把源文件删除查看链接文件是否有影响

[root@vipuser200 ~]# rm -rf ln.txt

[root@vipuser200 ~]# cat ln2.txt

hardlink

hardlink2

我们发现ln2.txt不受影响

#特点一：源文件被删除，不影响链接文件的正常使用

下面我们创建个目录的硬链接

[root@vipuser200 ~]# mkdir test

[root@vipuser200 ~]# ln test/ test1

ln: `test/': hard link not allowed for directory

#特点二：硬链接不能对目录创建

[root@vipuser200 ~]# ln /boot/vmlinuz-2.6.32-431.el6.x86_64 lnboot

ln: creating hard link `lnboot' => `/boot/vmlinuz-2.6.32-431.el6.x86_64': Invalid cross-device link

#特点三：硬链接不允许夸分区创建

注：不同分区可以通过df -h查看分区信息

[root@vipuser200 ~]# df -h

Filesystem Size Used Avail Use% Mounted on

/dev/sda2 9.9G 1.4G 8.0G 15% /

tmpfs 479M 0 479M 0% /dev/shm

/dev/sda1 194M 27M 158M 15% /boot

/dev/sr0 3.6G 3.6G 0 100% /mnt

软连接

简明概括软链接，就是类似于Windows的快捷方式。它实际上是一个特殊的文件。在符号链接中，文件实际上是一个文本文件，其中包含的有另一文件的位置信息。

ln -s命令可以创建软链接：

语法格式：ln -s源文件 目标文件

这里我们以图片展示更为直观

[root@vipuser200 ~]# cat ln3.txt

hardlink

hardlink2

我们删除源文件后查看

#特点一：删除后颜色变了，查看也没有信息

#特点二：可以对目录创建

#特点三：可以跨分区创建
