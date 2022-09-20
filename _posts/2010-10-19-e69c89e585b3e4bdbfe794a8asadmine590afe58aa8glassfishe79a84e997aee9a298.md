---
id: 2480
title: 有关使用asadmin启动Glassfish的问题
date: '2010-10-19T14:24:06+08:00'
author: Jay
layout: post
guid: 'http://jayxu.com/?p=2480'
permalink: /2010/10/19/2480
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
views:
    - '7179'
shorturl:
    - 'http://goo.gl/LktWv'
duoshuo_thread_id:
    - '6.3356046577584E+18'
dsq_thread_id:
    - '4277985860'
---

<!-- p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 13.0px 'Courier New'} p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 13.0px 'Courier New'; min-height: 15.0px} p.p3 {margin: 0.0px 0.0px 0.0px 0.0px; font: 13.0px Arial} p.p4 {margin: 0.0px 0.0px 0.0px 0.0px; font: 13.0px Arial; min-height: 15.0px} li.li3 {margin: 0.0px 0.0px 0.0px 0.0px; font: 13.0px Arial} ul.ul1 {list-style-type: disc} -->这个问题是在我们之前的一个项目中发现的，在这里与大家分享

一般在命令行下启动glassfish（3.0.x）有两种方法：
<ul>
	<li>先进入asadmin模式：${glassfish_home}/bin/asadmin。然后使用start-domain</li>
	<li>直接执行：${glassfish_home}/bin/asadmin start-domain domain1</li>
</ul>
对于第一种做法，会有一个很严重的问题：当使用ssh连接至远程主机，进入asadmin并执行start-domain后，如果没有在asadmin模式下执行exit退出（并显示“Command multimode executed successfully.”）而直接关闭ssh进程（直接kill、关闭console窗口或logout），会导致glassfish服务器终止（即使start-domain已成功），此问题已被稳定重现

因此，在这里提出建议：尽量使用第二种方法启动glassfish服务器；若使用第一种方法启动，请确保退出ssh进程前在asadmin下执行exit命令

针对glassfish版本：3.0.0及3.0.1