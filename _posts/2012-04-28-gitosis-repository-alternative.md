---
id: 13491
title: 'Gitosis Repository Alternative'
date: '2012-04-28T03:45:57+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13491'
permalink: /2012/04/28/13491
posturl_add_url:
    - 'yes'
views:
    - '4518'
duoshuo_thread_id:
    - '6.3356050312067E+18'
dsq_thread_id:
    - '4435135351'
---

今天Ubuntu放出了12.04更新，下午和刚才把linode和公司的11.10升了。升级过程很智能，基本不用怎么干预。本以为可以放心去睡了，谁知道公司服务器上的gitosis掉了链子，/usr/bin/gitosis-serve等三个gitosis的文件丢了，无法pull或push代码。于是按照<a href="http://progit.org/book/zh/ch4-7.html" target="_blank">这里</a>的方法安装gitosis，谁知道host gitosis的eagain.net拒绝访问，难道是全世界的程序员都在用gitosis把网站clone爆了？又google了很久，95%以上的结果用的都是eagain.net，这时才觉得云是多么的重要，这么重要的repository整个互联网上竟然只有一份……又过了20分钟，最终找打了一个替代网址：
<pre lang="bash">git clone https://github.com/tv42/gitosis.git</pre>
然后一切就OK了~

p.s. 马上五一了，抽空配个只读权限，把这个repository在我服务器上布一份

p.s.2 Ubuntu 12.04终于升级MySQL至5.5，Maven至3.0，赞一个