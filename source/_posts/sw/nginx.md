---
title: BAT都在用的Nginx到底是啥？
date: 2013/02/14 11:11:11
tags: "nginx"
---

如果你混迹IT圈儿，你可能听说过，或见过Nginx，IT技术人员对她都会有所耳闻，云计算工程师因为要应对负载均衡问题，需要更深入的了解Nginx，而Nginx也是百度、阿里、腾讯等企业IT架构中的常客。今天，笔者就与大家一起来探究一下，Nginx究竟是什么。

<!-- more -->

## Nginx是什么？

根据维基百科的定义，Nginx（发音同engine x）是一个网页服务器，它能反向代理HTTP，HTTPS，SMTP，POP和IMAP的协议链接，以及一个负载均衡器和一个HTTP缓存。

其初始版本发于12年前（2004年10月4日），起初只是供俄罗斯大型门户网站及搜索引擎Rambler（Рамблер）使用，后再2011年俄罗斯Nginx公司获得300万美元风投，也在国内外获得了大量的追随者，国内的BAT、新浪、搜狐都有应用，国外的Facebook、TechCrunch、Groupon和WordPress等公司，也是Nginx的簇拥。

技术创始人为为Igor Sysoev

此软件BSD-like协议下发行，可以在UNIX、GNU/Linux、BSD、Mac OS X、Solaris，以及Microsoft Windows等操作系统中均可运行。技术创始人为为Igor Sysoev。

## 特性如何

Nginx之所以能够受到世界各大互联网公司的青睐，当然是基于前面提过的在BSD-like协议下发行，更重要的还是Nginx拥有高性能的特点，主要体现在占用内存少，稳定性高等方面。

正因为这个特点，Nginx在四年前，就被某宝内部系统广泛使用。同时Nginx在处理并发服务能力方面十分优异，整体采用模块化设计，在处理负载均衡方面有着出色表现。根据Nginx的官方测试结果显示，Nginx可以支持五万个平行链接，而在实际运作中，可以支持2万至4万个平行链接。

## 架构如何

Nginx高性能的特点很大原因要归功于Nginx的架构与设计方式。当我们启动Nginx之后，会出现一个Master进程和多个Worker进程，Master进程主要用来管理Worker进程，放Worker进程异常退出后，会自动重新启动新的Worker进程。多个Worker进程之间是对等的，同时也是相互独立的。

Nginx架构图（图片来自网络）

另外，Nginx使用了最新的epoll和kqueue网络IO模型，这种模型在高并发的情况下，时间模型能够有更高的效率。与多线程相比，这种事件处理方式优势明显，能够不需要创建线程，每个请求占用的内存也很少，没有上下文切换，事件处理十分轻量级。

## 结束语

五年前，Nginx技术创始人做了家公司，冲击了微软IIS（互联网信息服务器Internet Information Server），如今，互联网在快速发展中，高并发、高负载情况愈加平常，Nginx依然焕发着自己的活力。
