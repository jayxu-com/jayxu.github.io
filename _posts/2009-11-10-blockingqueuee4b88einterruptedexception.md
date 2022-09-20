---
id: 1807
title: BlockingQueue与InterruptedException
date: '2009-11-10T13:10:00+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/?p=1807'
permalink: /2009/11/10/1807
aktt_notify_twitter:
    - 'no'
    - 'no'
dsq_thread_id:
    - '4322529994'
views:
    - '7250'
shorturl:
    - 'http://goo.gl/aY4pM'
duoshuo_thread_id:
    - '6.3356044686498E+18'
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>感谢Blader同学的抛砖</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>首先，这段代码会编译成功吗，运行起来会有异常吗，他会打印什么？</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

public class Foo {
   public static void main(String[] args) throws InterruptedException {
       BlockingQueue q = new LinkedBlockingQueue();
       q.put(1);
       Thread.currentThread().interrupt();
       System.out.println(q.take());
   }
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>运行后结果如下：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">Exception in thread "main" java.lang.InterruptedException
	at java.util.concurrent.locks.AbstractQueuedSynchronizer.acquireInterruptibly(AbstractQueuedSynchronizer.java:1135)
	at java.util.concurrent.locks.ReentrantLock.lockInterruptibly(ReentrantLock.java:312)
	at java.util.concurrent.LinkedBlockingQueue.take(LinkedBlockingQueue.java:354)
	at Foo.main(Foo.java:9)</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>看了一下源代码，阻塞队列的访问方法（take、put、poll、offer）会在执行之前检查Lock对象的中断标记，而Lock对象则是检查当前线程的中断标记</p>
<!-- /wp:paragraph -->