---
id: 1354
title: '在Tomcat 6中使用log4j'
date: '2009-01-20T12:15:00+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/2009/01/20/1354/'
permalink: /2009/01/20/1354
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
views:
    - '4300'
shorturl:
    - 'http://goo.gl/Qy2YI'
duoshuo_thread_id:
    - '6.3356042751414E+18'
dsq_thread_id:
    - '4374270448'
posturl_add_url:
    - 'yes'
---

Tomcat 6之前，在web应用中使用log4j还算容易，只要将log4j的jar包和相应的配置文件扔到项目的class path就齐活了。但是从6开始，一切变得如此复杂……
根据Tomcat 6 的<a href="http://tomcat.apache.org/tomcat-6.0-doc/logging.html" target="_blank">官方文档</a>，默认tomcat用的是JDK的logging框架，并配以“精简版”的common logging框架，即不支持common logging的底层框架自动切换功能，要使用log4j也就不可能了。要使用上述功能，需要使用“完整版”的common logging，而这个完整版的jar包apache上不提供下载，需要“自己编译tomcat代码”-_-|||，具体步骤如下：
<ol>
	<li>当然，你必须得有JDK、ant、SVN（如果你直接下载<a href="http://tomcat.apache.org/download-60.cgi" target="_blank">源代码包</a>，可以不需要SVN）</li>
	<li>从http://svn.apache.org/repos/asf/tomcat/tc6.0.x/ check out代码</li>
	<li>执行ant download</li>
	<li>执行ant（这里提一句，源代码的编码为utf8，直接编译的话会扔一堆warning，只要改一下ant脚本里的javac task就好了，加上encoding="utf8"）</li>
	<li>执行ant -f extras.xml</li>
	<li>将output/extras/<pre class="inline:true decode:1 " >tomcat-juli.jar覆盖到tomcat的bin目录下</pre></li>
	<li>将output/extras/tomcat-juli-adapters.jar拷到tomcat的lib目录下</li>
	<li>在lib目录下写tomcat的全局log4j配置</li>
	<li>在你的web项目中放入log4j.jar和log4j.properties(.xml)</li>
</ol>
<del datetime="2009-12-18T09:08:48+00:00">附：
tomcat-juli.jar
tomcat-juli-adapters.jar
使用utf8编译的build.xml</del>