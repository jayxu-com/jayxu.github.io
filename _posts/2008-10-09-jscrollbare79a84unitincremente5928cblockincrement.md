---
id: 747
title: JScrollBar的unitIncrement和blockIncrement
date: '2008-10-09T01:38:46+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/2008/10/09/747/'
permalink: /2008/10/09/747
aktt_notify_twitter:
    - 'yes'
    - 'yes'
dsq_thread_id:
    - '4271364235'
views:
    - '4199'
shorturl:
    - 'http://goo.gl/3KlGu'
duoshuo_thread_id:
    - '6.3356041927988E+18'
---

这两天在写swing的时候遇到一个问题，JScrollPane在相应鼠标滚轮的时候很慢，滚了一大段才移了一点点，给人的感觉就是鼠标很“硬”。刚才查了一下javadoc，看到JScrollbar有个方法：setUnitIncrement(int) 和 setBlockIncrement(int)。前一个是设置点击上下箭头的移动距离（也包括滚轮滚动），后一个是单击滚动条上空白处的移动距离，单位为像素。输出了一下unitIncrement的默认值，竟然是1 -_-|||。手动设为10，感觉鼠标终于灵活了……具体代码：
<pre lang="java">jScrollPane.getVerticalScrollBar().setUnitIncrement(10);</pre>
如果遇到和我相同问题的可以用上面的方法试一下。有点不爽的就是没有一个类似UIManager的全局变量可以设置，只能在各个JScrollBar上单独设置，有点麻烦。