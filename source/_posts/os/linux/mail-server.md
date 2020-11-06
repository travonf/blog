---
title: 自己本机搭建邮件服务器以及定制私人个性邮箱域名
date: 2010-06-01 20:10:40
updated: 2010-06-01 20:10:40
tags: "linux"
categories: "OS"
---

今天主要讲的是如何自己搭建邮件服务器，实现两个主机之间的邮件来往通信，工作中我们一般是用脚本搭建工具，但是为了明白其中的原理，我们自己手把手搭建一次，最后还会讲到如何如何定制自己公司域名的邮箱地址。

<!-- more -->

开班第十九天：

今天的课程大纲：

邮件服务器的认识

实现本地虚拟机和主机的邮件来往

dovecot实现支持pop3和imap

定制个性的私人域名邮箱

详细讲解：

邮件服务器的认识

认识邮件服务器，就要认识一下MUA、MDA、MTA，MUA是邮件客户端，就是我们最常接触到的一个层面；MDA是邮件分发代理， 它将决定你的邮件去向何方；MTA邮件传输代理，就是所谓的邮件服务器。邮件传输协议smtp，邮件接收协议pop3和imap ，今天我主要是自己搭建了一台DNS服务器来，然后通过两个主机来实现邮件来往。

实现本地虚拟机和主机的邮件来往

这里我先规定一下，我想要来往的两个邮件地址为root@itone.com和root@ittwo.com，DNS服务器地址为172.16.65.1，root@itone.com的ip为172.16.65.1，root@ittwo.com的ip为172.16.65.128.

1.首先是配置DNS服务器，能解析两个域名，具体过程我就不说了，我之前的教程里有的。

2.接着配置两个文件，我配置了其中一个，另一个同理

3.把DNS添加到两台主机的DNS文件中，然后进行测试。

4.测试成功后，配置itone.com和ittwo.com的postfix主配置文件，这里要改的地方有三个，一个是监听端口，一个是收件默认的主机名mydestination，最后一个是myorigin。监听端口改inet_interfaces = all，mydestination添加上自己的邮局域名，myorigin添加上自己是什么邮局，最后重启生效，service postfix restart.

5.发邮件测试。echo发送，测试成功！


常见的问题：端口只被本地监听，mx解析记录错误。

dovecot实现支持pop3和imap

我们如何实现支持pop3和imap，这里我们常用dovecot来实现，

1.安装dovecot，yum install dovecot

2.修改配置文件vim /etc/dovecot/conf.d/10-mail....，设置mail_location和mail_access_groups=mail。

3.这样呢，只要我们知道邮件服务器，就可以登录，然后狂发邮件，这样邮件服务器就变成了垃圾邮件服务器，所以我们在发邮件的时候也需要认证，这样就不会被人恶意发送邮件。vim /etc/postfix/main.cf，在最后添加如下内容：

4.注释/etc/dovecot/conf.d/10-master.conf里的postfix三行

5.重启服务，service postfix restart，service dovecot restart

定制个性的私人域名邮箱

现在很多公司都有自己的内部域名邮箱，什么叫域名邮箱，我们一般的邮箱就是qq.com，163.com，gmail.com等等，假如我们公司的网站域名是www.abc.com，那么我们的邮箱可以定位tom@abc.com，这样看起来会比较高大上一点，那么我们如何来实现呢？

1.首先要有公司自己的域名，这里我已经申请了xxxx.com

2.注册qq企业邮箱，这里注意，用的人越多，可能就要收费了。exmail.qq.com

3.然后就是为自己的域名添加一个mx记录，其实你注册企业邮箱的时候，他会手把手教你怎么弄的，我这里已经解析好了

4.设置自己企业邮箱的管理员账户，然后通过管理员账户添加各种子用户，这样你的个性域名邮箱就已经定制好了。

总结：

今天主要讲了邮件服务器的内容，邮件服务器作为一个linux中很重要的一部分，我们一定要好好掌握，另外就是如何在公司内部实现域名邮箱。
