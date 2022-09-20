---
id: 13791
title: '在Apache mpm-worker下跑PHP'
date: '2013-09-26T12:24:33+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13791'
permalink: /2013/09/26/13791
posturl_add_url:
    - 'yes'
views:
    - '4582'
duoshuo_thread_id:
    - '6.3356050863869E+18'
dsq_thread_id:
    - '4284716201'
---

worker相比较prefork的优势就不多说了，只说在ubuntu下通过fastcgi跑PHP的配置方案

先安装相关mod并启用
<blockquote>sudo apt-get install&nbsp;php5-cgi php5-cli&nbsp;fcgid

sudo a2enmod fcgid</blockquote>
然后修改需启用PHP的virtualhost相关配置文件
<pre class="inline:true lang:apache decode:1 " >Options +ExecCGI
AddHandler fcgid-script .php
FCGIWrapper /usr/lib/cgi-bin/php5 .php</pre>
reload Apache