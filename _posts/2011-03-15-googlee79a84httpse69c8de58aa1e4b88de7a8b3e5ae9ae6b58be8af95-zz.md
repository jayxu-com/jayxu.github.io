---
id: 10545
title: 'Google的HTTPS服务不稳定测试 [zz]'
date: '2011-03-15T23:05:09+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=10545'
permalink: /2011/03/15/10545
follow5:
    - 'true'
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
dsq_thread_id:
    - '4469125710'
views:
    - '4596'
shorturl:
    - 'http://goo.gl/7vOED'
duoshuo_thread_id:
    - '6.3356047820021E+18'
---

转自：<a href="http://www.williamlong.info/archives/2579.html" target="_blank">月光博客</a>

我的观点是：
<ol>
	<li>迫使用户完全放弃使用难以被窃听邮件内容的gmail，或者</li>
	<li>迫使用户退让而使用可以被窃听的http协议访问gmail</li>
	<li>这招相当丧心病狂</li>
</ol>
以下是原文

从<a href="http://www.williamlong.info/archives/2558.html" target="_blank">2011年3月2日</a>开始，人们发现从国内访问很多Google的HTTPS服务（以下简称服务）开始出现不稳定现象，很多人怀疑是Google的服务或网络不稳定所致。本文通过技术测试的方法发现服务不稳定的根本原因。

为了测试服务不稳定的原因，我们使用了2台VPS服务器，一台在上海，一台在香港。这2台VPS服务器上分别运行测试程序，对Google的HTTP服务和Google的HTTPS服务同时进行测试。

我们同时测试HTTP和HTTPS服务可以区分是否是Google的服务本身不稳定：如果是Google的服务本身不稳定，那么HTTP和HTTPS服务应该同时不正常。即使HTTPS所需要的服务器资源比较多也是在加密解密TCP连接中的数据的开销费，在TCP连接建立之前HTTP和HTTPS对服务器的资源开销是一致的。也就是说在很短的时间内，如果出现大量HTTP协议的80端口能正常连接，而HTTPS的443端口无法正常连接的情况，就不是Google服务不稳定造成的。

在同一时间，我们使用香港的VPS进行测试，这样就能看到是国内网络的问题还是非国内网络的问题导致的。如果是非国内网络的问题，上海和香港应该同时出现服务不稳定的现象。结合这2者测试，我们就可知道是否是Google服务或者网络不正常了。

测试程序代码可以在<a href="https://code.google.com/p/gfwtest/" target="_blank">这里</a>找到，配置的各个参数可以在<a href="https://code.google.com/p/gfwtest/wiki/parameter_list" target="_blank">这里</a>找到，本次测试的配置为5秒进行1次测试，连续测试1个小时，测试结果可以看在<a href="https://code.google.com/p/gfwtest/downloads/list" target="_blank">这里</a>的2个log文件和编译好的Java程序。（这几个链接很多时候需要国外IP才能访问）

从上海的测试结果的log文件中我们可以看到，HTTP服务基本正常，而HTTPS服务时常连接失败，摘录一小段log如下：
<blockquote>Start in： 2011-03-15 14：50：01 +0800    End in： 2011-03-15 14：50：01 +0800    Status： Success    URL： https://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：06 +0800    End in： 2011-03-15 14：50：06 +0800    Status： Success    URL： http://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：16 +0800    End in： 2011-03-15 14：50：16 +0800    Status： Success    URL： http://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：26 +0800    End in： 2011-03-15 14：50：26 +0800    Status： Success    URL： http://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：11 +0800    End in： 2011-03-15 14：50：32 +0800    Status： Connection timed out： connect    URL： https://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：36 +0800    End in： 2011-03-15 14：50：36 +0800    Status： Success    URL： http://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：21 +0800    End in： 2011-03-15 14：50：42 +0800    Status： Connection timed out： connect    URL： https://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：46 +0800    End in： 2011-03-15 14：50：46 +0800    Status： Success    URL： http://www.google.com/images/logos/ps_logo2.png

Start in： 2011-03-15 14：50：31 +0800    End in： 2011-03-15 14：50：52 +0800    Status： Connection timed out： connect    URL： https://www.google.com/images/logos/ps_logo2.png</blockquote>
从上海的测试结果的整个log文件中我们可以看到，HTTPS服务连接失败的周期为15分钟左右，15分钟正常访问服务，15分钟TCP协议无法建立连接，周而复始。而同时香港的测试结果全部可以正常访问服务。

由此，我们可以得出结论：在国内到Google的HTTPS服务中的某个路由器上，周期性地阻断Google服务器的HTTPS端口443，从而人为劣化Google的服务，进而导致使用Google服务的人慢慢减少。

来源：davidsky投稿。