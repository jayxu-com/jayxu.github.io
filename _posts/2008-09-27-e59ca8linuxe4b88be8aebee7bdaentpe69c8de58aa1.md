---
id: 731
title: 在Linux下设置ntp服务
date: '2008-09-27T16:35:37+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/2008/09/27/731/'
permalink: /2008/09/27/731
aktt_notify_twitter:
    - 'yes'
    - 'yes'
views:
    - '4064'
shorturl:
    - 'http://goo.gl/IwLUD'
duoshuo_thread_id:
    - '6.3356041922787E+18'
dsq_thread_id:
    - '4354576709'
---

节省时间，什么是ntp在这里就不解释了，下面就大概讲一下在Linux下如何配置、启动ntp服务。当然，前提是在系统中已经安装了ntp服务

首先手动同步一下时间：
<pre lang="bash"># ntpdate  222.73.214.125</pre>
其中222.73.214.125是ntp服务器的IP，<a href="http://www.pool.ntp.org/en/" target="_blank">这里</a>可以找到一堆的ntp服务器，挑一个国内的就行了

同步后使用date命令验证当前时间，如果不对需要配置系统时区。然后修改/etc/ntp.config文件，将刚才选择的ntp服务器添加进去，语法为：
<pre lang="bash">server 222.73.214.125</pre>
最后在系统服务中启动ntp：
<pre lang="bash"># /etc/init.d/ntpd start
# chkconfig --level 35 ntpd on</pre>