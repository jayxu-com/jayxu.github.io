---
id: 844
title: '如何cancel一个swing worker（续）'
date: '2008-11-14T23:35:19+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/?p=844'
permalink: /2008/11/14/844
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
dsq_thread_id:
    - '4271365742'
views:
    - '3422'
shorturl:
    - 'http://goo.gl/xF3NU'
duoshuo_thread_id:
    - '6.3356042164337E+18'
---

上一次谈到如何去cancel一个swing worker，今天在代码里又出了问题：即使使用swingWorker.cancel(true)仍然无法在sleep时中止线程。追了一下代码，最后在javax.swing.ImageIcon类里找到了原因：
<pre lang="java" line="1">
protected void loadImage(Image image) {
    synchronized(tracker) {
        int id = getNextID();

        tracker.addImage(image, id);
	try {
	    tracker.waitForID(id, 0);
	} catch (InterruptedException e) {
	    System.out.println("INTERRUPTED while loading Image");
	}
        loadStatus = tracker.statusID(id, false);
	tracker.removeImage(image, id);

        width = image.getWidth(imageObserver);
	height = image.getHeight(imageObserver);
    }
}
</pre>
其中第7行会抛出InterruptedException，而在第10行捕捉了该异常，导致InterruptedException无法抛到我的代码里。很典型的“eat-up exception”的例子。解决该问题可以在初始化ImageIcon前sleep一下，比如sleep(5)，让interrupted状态在sleep中触发InterruptedException