---
id: 10588
title: '在Web上运行Linux [zz]'
date: '2011-05-19T12:30:56+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=10588'
permalink: /2011/05/19/10588
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
views:
    - '4705'
shorturl:
    - 'http://goo.gl/OLZg9'
duoshuo_thread_id:
    - '6.3356047823712E+18'
dsq_thread_id:
    - '4447900650'
hefo_before:
    - '0'
hefo_after:
    - '0'
posturl_add_url:
    - 'yes'
---

原文来自<a href="http://coolshell.cn/articles/4722.html" target="_blank">酷壳</a>

一个叫Fabrice Bellard的程序员写了一段Javascript在Web浏览器中启动Linux（<a href="http://bellard.org/jslinux/" target="_blank">原网页</a>，我把这个网页iframe在了下面），目前，你只能使用Firefox 4和Chrome 11运行这个Linux。这不是什么假的模仿Linux的东西，这是实实在在的运行一个Linux。这一举动还引起了很多很牛人的关注，包括Javascript的创建者<a href="http://twitter.com/#!/BrendanEich/status/70393502328045568" target="_blank">Brendan Eich</a>。

<!--iframe frameborder="0" height="600" id="1kjs" src="http://bellard.org/jslinux/" style="background-image: initial; background-attachment: initial; background-origin: initial; background-clip: initial; background-color: rgb(0, 0, 0); border-top-width: 0px; border-right-width: 0px; border-bottom-width: 0px; border-left-width: 0px; border-style: initial; border-color: initial; background-position: initial initial; background-repeat: initial initial; " width="550"></iframe-->

（由于该JS对浏览器性能较大，我已将iframe注释，有兴趣的同学可去上面的原站地址查看）

随后，Fabrice Bellard发布了相关的技术说明：<a href="http://bellard.org/jslinux/tech.html" target="_blank">http://bellard.org/jslinux/tech.html</a>，从这份文档中我们可以看到：
<ul>
 	<li>这个模似器完全由Javascript写成</li>
 	<li>CPU仿真器使用的是<a href="http://wiki.qemu.org/Main_Page">QEMU</a>（接近于原古的486），为了装上Linux，其做了一些改动。</li>
 	<li>Javascript的终端本来可以使用<a href="http://www.masswerk.at/termlib/">termlib</a>，但他还是自己写了一个，因为OS的按键和Web浏览器不一样（<a href="http://unixpapa.com/js/key.html">here</a>）</li>
 	<li>Linux  使用了2.6.20内核，编译配置在<a href="http://bellard.org/jslinux/config_linux-2.6.20" target="_blank">这里</a>，并做了一些<a href="http://bellard.org/jslinux/patch_linux-2.6.20" target="_blank">小改动</a>。</li>
 	<li>磁盘用的是Ram Disk，在启动的时候装载。其文件系统由<a href="http://buildroot.uclibc.org/">Buildroot</a> 和<a href="http://www.busybox.net/">BusyBox</a>产生。</li>
 	<li>在Home目录下有一个hello.c的程序，你可以使用<a href="http://bellard.org/tcc/">TinyCC</a>编译（tcc，参看酷壳的<a title="用TCC可以干些什么？" href="http://coolshell.cn/articles/786.html" target="_blank">这篇文章</a>）</li>
</ul>
从这个事我有这些感触，
<ol>
 	<li>在Web上运行一个Linux的操作系统不是问题。那么在Web上还有什么不能做的吗？</li>
 	<li>Linux真是性能很高，在Javascript下运行感觉也不慢啊。</li>
 	<li>真是Techno-Geek。</li>
</ol>