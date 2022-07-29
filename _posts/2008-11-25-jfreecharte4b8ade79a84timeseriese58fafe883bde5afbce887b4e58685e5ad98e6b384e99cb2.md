---
id: 1233
title: JFreeChart中的TimeSeries可能导致内存泄露
date: '2008-11-25T14:40:01+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/2008/11/25/1233/'
permalink: /2008/11/25/1233
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
dsq_thread_id:
    - '4271362572'
views:
    - '6306'
shorturl:
    - 'http://goo.gl/7y4u6'
duoshuo_thread_id:
    - '6.3356042421322E+18'
posturl_add_url:
    - 'yes'
image: 'https://d1k8eqsfs47rrv.cloudfront.net/log/wp-content/uploads/2008/11/mem_heap.png'
---

前段时间说到现在的项目里在用JFreeChart。昨天晚上走之前没把客户端关掉，今天中午到公司发现程序已经崩了，狂抛OutOfMemoryError。用NB的profiler跟了一下，发现是JFreeChart或者说是没有正确使用JFreeChart的TimeSeries导致的后果
TimeSeries有一个方法setMaximumItemAge：
<pre class="lang:java decode:1 " >
public void setMaximumItemAge(long periods)</pre>
该方法文档如下：
<blockquote>
<dl>
 	<dd>Sets the number of time units in the 'history' for the series. This provides one mechanism for automatically dropping old data from the time series. For example, if a series contains daily data, you might set the history count to 30. Then, when you add a new data item, all data items more than 30 days older than the latest value are automatically dropped from the series.</dd>
 	<dd></dd>
 	<dd>
<dl>
 	<dt><strong>Parameters:</strong></dt>
 	<dd><pre class="inline:true decode:1 " >periods</pre> - the number of time periods.</dd>
 	<dt></dt>
</dl>
</dd>
</dl>
</blockquote>
maximumItemAge的默认值为Long.MAX_VALUE，因此如果不设置该值的话在可预见的未来过期数据将不会被丢弃，这样会导致TimeSeries的数据越来越大，尤其是在设置axis.setAutoRange(true);和axis.setFixedAutoRange(DATA_AGE);后（将横轴设为固定长度，图表只容纳限定数目个点，视觉上就是数据从右边“推入”图表，从左侧被“推出”）。虽然视觉上数据只有那么一点，但是从图表上消失的“旧”数据并没有从series里清除，导致最终的内存不足

<a href="http://jayxu.com/log/wp-content/uploads/2008/11/mem_heap_3.png"><img class="alignnone size-medium wp-image-1236" title="mem_heap_2" src="http://jayxu.com/log/wp-content/uploads/2008/11/mem_heap_3.png" alt="" width="436" height="278" /></a>

未使用setMaximumItemAge的堆分布，才2分钟就开始深度GC，且堆大小已经开始扩大

<a href="http://jayxu.com/log/wp-content/uploads/2008/11/mem_gc_2.png"><img class="alignnone size-medium wp-image-1237" title="mem_gc_2" src="http://jayxu.com/log/wp-content/uploads/2008/11/mem_gc_2.png" alt="" width="436" height="278" /></a>

未使用setMaximumItemAge的对象年龄（代），曲线很陡，说明很多对象没有被回收

<a href="http://jayxu.com/log/wp-content/uploads/2008/11/mem_heap.png"><img class="alignnone size-medium wp-image-1238" title="mem_heap" src="http://jayxu.com/log/wp-content/uploads/2008/11/mem_heap.png" alt="" width="436" height="278" /></a>

使用setMaximumItemAge的堆分布，堆内存占用比较缓慢，堆大小未扩大，未进行深度GC

<a href="http://jayxu.com/log/wp-content/uploads/2008/11/mem_gc.png"><img class="alignnone size-medium wp-image-1239" title="mem_gc" src="http://jayxu.com/log/wp-content/uploads/2008/11/mem_gc.png" alt="" width="436" height="278" /></a>

使用setMaximumItemAge的对象年龄（代），数值很高，是因为还没有进行深度GC的原因

在此提醒正在使用JFreeChart尤其是TimeSeries的给位，千万记得设置maximumItemAge