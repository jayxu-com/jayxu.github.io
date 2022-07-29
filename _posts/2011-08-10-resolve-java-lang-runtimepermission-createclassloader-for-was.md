---
id: 11623
title: 'Resolve &#8220;Access denied (java.lang.RuntimePermission createClassLoader)&#8221; for WAS'
date: '2011-08-10T12:03:36+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=11623'
permalink: /2011/08/10/11623
aktt_notify_twitter:
    - 'yes'
views:
    - '8148'
aktt_tweeted:
    - '1'
shorturl:
    - 'http://goo.gl/8XC5W'
duoshuo_thread_id:
    - '6.3356048551759E+18'
dsq_thread_id:
    - '4270617658'
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

In my current project deploying Insight to WAS, I got the following exception when trying to access Insight:
<pre>[8/7/11 21:51:09:639 CDT] 00000033 webapp        E com.ibm.ws.webcontainer.webapp.WebApp logError SRVE0293E: [Servlet Error]-[javax.servlet.ServletException: SRVE0207E: Uncaught initialization exception created by servlet]: java.security.AccessControlException: Access denied (java.lang.RuntimePermission createClassLoader)
        at java.security.AccessController.checkPermission(AccessController.java:108)
        at java.lang.SecurityManager.checkPermission(SecurityManager.java:533)
        at com.ibm.ws.security.core.SecurityManager.checkPermission(SecurityManager.java:211)
        at java.lang.SecurityManager.checkCreateClassLoader(SecurityManager.java:595)
        at java.lang.ClassLoader.(ClassLoader.java:145)
        at java.security.SecureClassLoader.(SecureClassLoader.java:52)
        at java.net.URLClassLoader.(URLClassLoader.java:198)
        at com.cognos.pogo.isolation.ParanoidClassLoader.(ParanoidClassLoader.java:95)
        at com.cognos.pogo.isolation.ParanoidClassLoader$3.run(ParanoidClassLoader.java:137)
        at java.security.AccessController.doPrivileged(AccessController.java:202)
        at com.cognos.pogo.isolation.ParanoidClassLoader.newInstance(ParanoidClassLoader.java:135)
        at com.cognos.pogo.isolation.ServletWrapper.getParanoidClassLoader(ServletWrapper.java:304)
        at com.cognos.pogo.isolation.ServletWrapper.getClassLoader(ServletWrapper.java:183)
        at com.cognos.pogo.isolation.ServletWrapper.init(ServletWrapper.java:87)
        at com.ibm.ws.webcontainer.servlet.ServletWrapper.init(ServletWrapper.java:358)
        at com.ibm.ws.webcontainer.servlet.ServletWrapperImpl.init(ServletWrapperImpl.java:168)
        at com.ibm.ws.webcontainer.servlet.ServletWrapper.handleRequest(ServletWrapper.java:737)
        at com.ibm.ws.webcontainer.servlet.ServletWrapper.handleRequest(ServletWrapper.java:500)
        at com.ibm.ws.webcontainer.servlet.ServletWrapperImpl.handleRequest(ServletWrapperImpl.java:178)
        at com.ibm.ws.webcontainer.webapp.WebAppRequestDispatcher.forward(WebAppRequestDispatcher.java:341)
        at com.ibm.ws.webcontainer.extension.DefaultExtensionProcessor.handleRequest(DefaultExtensionProcessor.java:709)
        at com.ibm.ws.webcontainer.webapp.WebApp.handleRequest(WebApp.java:3810)
        at com.ibm.ws.webcontainer.webapp.WebGroup.handleRequest(WebGroup.java:276)
        at com.ibm.ws.webcontainer.WebContainer.handleRequest(WebContainer.java:931)
        at com.ibm.ws.webcontainer.WSWebContainer.handleRequest(WSWebContainer.java:1583)
        at com.ibm.ws.webcontainer.channel.WCChannelLink.ready(WCChannelLink.java:183)
        at com.ibm.ws.http.channel.inbound.impl.HttpInboundLink.handleDiscrimination(HttpInboundLink.java:455)
        at com.ibm.ws.http.channel.inbound.impl.HttpInboundLink.handleNewInformation(HttpInboundLink.java:384)
        at com.ibm.ws.http.channel.inbound.impl.HttpICLReadCallback.complete(HttpICLReadCallback.java:83)
        at com.ibm.ws.tcp.channel.impl.AioReadCompletionListener.futureCompleted(AioReadCompletionListener.java:165)
        at com.ibm.io.async.AbstractAsyncFuture.invokeCallback(AbstractAsyncFuture.java:217)
        at com.ibm.io.async.AsyncChannelFuture.fireCompletionActions(AsyncChannelFuture.java:161)
        at com.ibm.io.async.AsyncFuture.completed(AsyncFuture.java:138)
        at com.ibm.io.async.ResultHandler.complete(ResultHandler.java:204)
        at com.ibm.io.async.ResultHandler.runEventProcessingLoop(ResultHandler.java:775)
        at com.ibm.io.async.ResultHandler$2.run(ResultHandler.java:905)
        at com.ibm.ws.util.ThreadPool$Worker.run(ThreadPool.java:1550)
</pre>
After some research on the Internet, the issue was fixed by adding the following code to /opt/ibm/RationalInsight/AppServer/profiles/RationalReport/properties/server.policy:
<pre>grant {
    permission java.security.AllPermission;
};</pre>