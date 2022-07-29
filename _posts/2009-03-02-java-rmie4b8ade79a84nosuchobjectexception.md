---
id: 1425
title: 'Java RMI中的NoSuchObjectException'
date: '2009-03-02T11:08:17+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/2009/03/02/1425/'
permalink: /2009/03/02/1425
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
views:
    - '6451'
shorturl:
    - 'http://goo.gl/v8uC5'
duoshuo_thread_id:
    - '6.335604297128E+18'
dsq_thread_id:
    - '4302340078'
posturl_add_url:
    - 'yes'
---

最近项目里的RMI在Linux下运行老出问题，而且问题出得还很不稳定。那个程序启动时会分别在4个端口上绑定4个相同的对象，结果就是有时绑定成功3个，有时候才1个……查看log，抛出下面异常
<blockquote>java.rmi.NoSuchObjectException: no such object in table</blockquote>
上网搜了一下，<a href="http://forums.oracle.com" target="_blank">这篇</a>文章给出了原因和解决方法：我在代码中做RMI绑定的时候用的是局部变量：
<pre class="lang:java decode:1 " >registry.rebind(name, UnicastRemoteObject.exportObject(new RemoteObject(), 0));</pre>
该局部变量在服务器端被GC后客户端再远程调用方法便会抛出上述异常。解决方法很简单，使用对远程对象的强引用以防止对象被GC，比如把局部引用改为类静态引用