---
id: 2424
title: '有关PWC4011: Unable to set request character encoding to UTF-8'
date: '2010-09-27T15:04:52+08:00'
author: Jay
layout: post
guid: 'http://jayxu.com/?p=2424'
permalink: /2010/09/27/2424
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
views:
    - '6776'
dsq_thread_id:
    - '4444358819'
shorturl:
    - 'http://goo.gl/XoLRR'
posturl_add_url:
    - 'yes'
duoshuo_thread_id:
    - '6.3356046334272E+18'
---

最近在使用Glassfish 3作为项目容器的时候发现一个问题：我们在项目中使用Filter对请求进行了拦截，对其进行编码转换。之前在tomcat时代这一做法没有任何问题，但是到了GF下，每次访问某些页面时控制台总会输出
<blockquote>警告: PWC4011: Unable to set request character encoding to UTF-8 from context , because request parameters have already been read, or ServletRequest.getReader() has already been called</blockquote>
有时一输出就是一大片，相当烦人。在网上搜了一圈，结果少得可怜，基本都是java.net若干年前的讨论，主要的两个thread在下面（其中fidodido就是我）：

<del><a href="https://community.oracle.com/community/java" target="_blank">http://forums.java.net/jive/thread.jspa?threadID=35821</a></del>

<del><a href="http://forums.java.net/jive/thread.jspa?threadID=42899" target="_blank">http://forums.java.net/jive/thread.jspa?threadID=42899</a></del>

<a href="http://www.java.net/node/673881" target="_blank">http://www.java.net/node/673881</a>

顺着其中的一个链接最终找到了这个wiki：<a href="http://wikis.sun.com/display/glassfish/FaqWebAppUnableToSetRequestCharEncoding" target="_blank">http://wikis.sun.com/display/glassfish/FaqWebAppUnableToSetRequestCharEncoding</a>，可到了仍没有解释清楚，而是通过调高日志级别使其不输出而已。也罢，至少眼不见心不烦

这里给个截屏，是在GF的admin console中直接修改日志级别的方法，省得vim了

<a href="http://jayxu.com/log/wp-content/uploads/2010/09/Module-Log-Levels.png"><img class="alignnone size-medium wp-image-2425" title="Module Log Levels" src="http://jayxu.com/log/wp-content/uploads/2010/09/Module-Log-Levels.png" alt="" width="480" height="332" /></a>