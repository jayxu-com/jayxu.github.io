---
id: 1557
title: '不用翻墙访问YouTube的方法 [zz]'
date: '2009-07-02T10:18:32+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/?p=1557'
permalink: /2009/07/02/1557
aktt_notify_twitter:
    - 'no'
    - 'no'
dsq_thread_id:
    - '4271360676'
views:
    - '18129'
shorturl:
    - 'http://goo.gl/Ck1fT'
duoshuo_thread_id:
    - '6.3356043965917E+18'
posturl_add_url:
    - 'yes'
---


<blockquote>Youtube 被 GFW 做了 DNS 劫持并 X 掉了国外的 IP，但是 google.cn 有 Youtube 的镜像呆在墙内，至今安全，我太后知后觉了。只需将这些镜像服务器的 IP 填入 host 文件，即可不用翻墙看 Youtube了。方法如下

用记事本打开 C:\WINDOWS\system32\drivers\etc\hosts 文件，在下面添加两行谷歌中国的 IP 地址指向 www.youtube.com 和 gdata.youtube.com 就可以不用翻墙访问 YouTube。

开始 -&gt; 运行 cmd 输入 nslookup www.google.cn 可获得几个 IP 都可以使用（不要用国外 DNS，获得的是国外 IP） 。

例如添加下面2个：
203.208.39.104 www.youtube.com
203.208.33.100 gdata.youtube.com

需要上传添加：
203.208.39.99 upload.youtube.com

可选：
203.208.39.99 insight.youtube.com
203.208.39.160 help.youtube.com
203.208.39.104 youtube.com</blockquote>
<a href="http://blog.redren.com/2009/06/climbing-over-the-wall-do-not-have-access-to-youtubes-approach-to/" target="_blank" rel="noopener">原文链接</a>

补充：貌似大家和搜索引擎对这篇博很感兴趣，那给大家个<a href="http://www.youtubecn.com/" target="_blank" rel="noopener">链接</a>，一位网友自己搭的youtube，墙内可访问