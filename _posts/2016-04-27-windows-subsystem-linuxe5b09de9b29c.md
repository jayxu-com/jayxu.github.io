---
id: 14916
title: 'Windows Subsystem for Linux（WSL）尝鲜'
date: '2016-04-27T15:04:30+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=14916'
permalink: /2016/04/27/14916
posturl_add_url:
    - 'yes'
views:
    - '4385'
dsq_thread_id:
    - '4780248267'
duoshuo_thread_id:
    - '6.335605270886E+18'
image: 'https://d1k8eqsfs47rrv.cloudfront.net/log/wp-content/uploads/2016/04/73868-20160408011440015-662314838.jpg'
---

今天试了下Windows 10从14316预览版本开始加入的WSL下的bash环境，<a href="http://www.cnblogs.com/lazio10000/p/5366350.html" target="_blank">这里</a>有一篇简单的介绍和启用方式

[gallery type="rectangular" ids="14917,14918,14919,14920,14921,14922,14923,14924"]

简单的总结：
<ul>
<li>我的win 10版本：insider preview 14328</li>
<li>基于Ubuntu Trusty（14.04），内核版本3.4.0</li>
<li>可以使用大多数linux命令，包括vim、apt-get</li>
<li>gnome环境无法启动</li>
<li>磁盘映射不完善，df、fdisk无法列出磁盘列表</li>
<li>systemd、udev不支持</li>
</ul>