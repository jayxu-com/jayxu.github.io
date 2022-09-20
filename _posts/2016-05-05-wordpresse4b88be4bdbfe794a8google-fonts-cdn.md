---
id: 14961
title: 'WordPress下使用Google Fonts CDN'
date: '2016-05-05T20:35:24+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=14961'
permalink: /2016/05/05/14961
posturl_add_url:
    - 'yes'
views:
    - '3441'
dsq_thread_id:
    - '4802110305'
duoshuo_thread_id:
    - '6.3356052711418E+18'
image: 'https://d1k8eqsfs47rrv.cloudfront.net/log/wp-content/uploads/2016/05/u2252188009881490895fm21gp0.jpg'
---

由于众所周知的原因，google所有的应用、服务在国内无法使用，包括google fonts。如果你的wordpress（默认）使用了google fonts，那对于新访用户带来的延迟不言而喻。今天下班后打算解决这个问题，在网上转了一圈之后，发现大多数的搜索结果都建议使用<a href="http://libs.useso.com" target="_blank">360的CDN</a>，在这件事情上360的确是个活雷锋。但是，如果你的站点和我的一样默认使用https协议，那很不幸，这个CDN无法使用，原因是<a href="https://libs.useso.com" target="_blank">https://libs.useso.com</a>使用了非安全的https协议：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/05/无法加载_https___libs_useso_com_.png"><img class="alignnone size-medium wp-image-14963" src="http://www.jayxu.com/log/wp-content/uploads/2016/05/无法加载_https___libs_useso_com_-600x654.png" alt="无法加载_https___libs_useso_com_" width="600" height="654" /></a>
于是又在网上搜了一大圈，最后在google的帮助下，找到了另一个（支持https协议的）活雷锋：<a href="https://servers.ustclug.org/2014/06/blog-googlefonts-speedup/" target="_blank">科大 LUG</a>～

CDN找到了，接下来就是替换wordpress里的地址了，这里借用了360 CDN上推荐的插件<a href="http://www.soulteary.com/2014/06/08/replace-google-fonts.html">Replace Google Fonts</a>。安装后直接修改插件代码，将replace-google-fonts.php中的CDN地址替换掉：
<pre class="lang:php decode:1 " >public function ohMyFont($text)
{
    return str_replace('//fonts.googleapis.com/', '//fonts.useso.com/', $text);
}</pre>
修改为
<pre class="lang:php decode:1 " >public function ohMyFont($text)
{
    return str_replace('//fonts.googleapis.com/', '//fonts.lug.ustc.edu.cn/', $text);
}</pre>
然后，世界瞬间就美好了～