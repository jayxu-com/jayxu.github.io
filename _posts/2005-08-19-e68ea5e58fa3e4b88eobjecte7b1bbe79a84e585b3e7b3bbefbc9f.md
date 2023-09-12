---
id: 15963
title: 接口与Object类的关系？
date: '2005-08-19T13:53:30+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15963'
permalink: /2005/08/19/15963
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '2207'
dsq_thread_id:
    - '5274804421'
---

今天凌晨coding的时候发现一个很有趣的现象。“Object类是Java体系的单根父节点，所有Java类都从Object类继承。”这句话是大部分green hand都知道的Java金句，毋庸置疑。那如果我问你接口和Object类的关系呢？答案是“没有关系”。请看下面的代码：
<pre lang="java">
Map map = new HashMap();
map.clone();
</pre>

Map是一个接口，HashMap是一个类。clone()方法在Object类中定义，因此我下意识认为第二行可以这么写。结果编译器报错：clone()方法未定义。这个错误让我很郁闷，看了半天doc才发祥原来Map是一个接口，而接口和Object类没有任何关系，所以Map也就没有继承clone()。于是把代码改成下面的样子：
<pre lang="java">
HashMap map = new HashMap();
map.clone();
</pre>

这样就可以了。