---
id: 713
title: 如何在Java的enum中使用annotation
date: '2008-09-22T23:14:59+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/2008/09/22/713/'
permalink: /2008/09/22/713
aktt_notify_twitter:
    - 'yes'
    - 'yes'
dsq_thread_id:
    - '4271360286'
views:
    - '3695'
shorturl:
    - 'http://goo.gl/Kk9Us'
duoshuo_thread_id:
    - '6.3356041704893E+18'
---

刚才在写一个方法的时候试图在enum上使用annotation：
<pre lang="java">
public enum DataKey {
    @Incremental
    @FromProbe
    @Transient(replacePolicy = ReplacePlolicy.REPLACE_IF_LATER_THAN)
    VISIT_COUNT
}
</pre>
然后在merge的时候使用annotation：
<pre lang="java">if (key.getClass().isAnnotationPresent(Transient.class)) {
    ...
}</pre>
结果不进if，debug时发现key（DataKey的对象）的类型是DataKey（其实也挺顺理成章的），于是使用如下代码：
<pre lang="java">if (DataKey.class.getField(key.name()).isAnnotationPresent(Transient.class)) {
    ...
}</pre>
结果正确。
结论：在对enum类型使用FIELD一级annotation时需要使用第二种方法进行反射