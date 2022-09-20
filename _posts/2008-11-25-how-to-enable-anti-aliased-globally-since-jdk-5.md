---
id: 1243
title: 'How To Enable Anti-Aliased Globally Since JDK 5'
date: '2008-11-25T17:51:56+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/2008/11/25/1243/'
permalink: /2008/11/25/1243
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
views:
    - '3266'
shorturl:
    - 'http://goo.gl/pcXhy'
duoshuo_thread_id:
    - '6.3356042421952E+18'
dsq_thread_id:
    - '4427303570'
---

I just read "Swing Hacks" and find it is that easy to enable anti-aliased since JDK 5.  Just add a one-line code listed below at the very beginning of your whole application
<pre lang="java">System.setProperty("swing.aatext", "true");</pre>
That's all