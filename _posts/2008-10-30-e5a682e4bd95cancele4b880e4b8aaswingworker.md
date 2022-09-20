---
id: 764
title: 如何cancel一个swingworker
date: '2008-10-30T16:04:37+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/2008/10/30/764/'
permalink: /2008/10/30/764
aktt_notify_twitter:
    - 'yes'
    - 'yes'
views:
    - '4183'
shorturl:
    - 'http://goo.gl/M0oZP'
duoshuo_thread_id:
    - '6.3356041929079E+18'
dsq_thread_id:
    - '4463104424'
---

最近在项目里一直在用jdesktop的swingworker（已经合入JDK 6），是个不错的swing线程库。今天需要在界面里cancel一个swingworker。研究了一下午，结合swingworker的文档、源代码和自己的代码实验，以下是两种安全cancel一个swingworker的方法

方法一，使用isCancelled：
<pre lang="java">protected Object doInBackground() throws Exception {
    while (!isCancelled()) {
       ...
    }

    return null;
}</pre>
需要cencel时调用swingworker.cancel(false)，不中断线程，只置cancel标记。

方法二，使用sleep：
<pre lang="java">protected Object doInBackground() throws Exception {
    while (running) {
        ...
        sleep(30);
    }

    return null;
}</pre>
需要cencel时调用swingworker.cancel(true)，在sleep处中断线程。切记，不需要捕捉sleep抛出的InterruptedException，swingworker会处理该异常。