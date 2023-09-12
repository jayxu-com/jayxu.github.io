---
id: 1570
title: 'Which GlassFish version is right for me? [zz]'
date: '2009-07-18T01:57:55+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/2009/07/18/1570/'
permalink: /2009/07/18/1570
aktt_notify_twitter:
    - 'no'
    - 'no'
views:
    - '3707'
shorturl:
    - 'http://goo.gl/bh4lu'
duoshuo_thread_id:
    - '6.3356043967762E+18'
posturl_add_url:
    - 'yes'
dsq_thread_id:
    - '4926457602'
---

GlassFish has several versions that you may have heard of. Each one attempts to address different needs. I've had several people in the last couple of weeks ask me which one they should use, so here's a quick list of features and reasons to use one more than the other.

• <strong>GlassFish v2.1</strong>: current JavaEE 5-certified and supported product. Offers centralized admin, clustering. v2.0 was released in September 2007 and v2.1 in March 2009 with the <a href="http://blogs.oracle.com/nazrul/entry/glassfish_enterprise_manager">Enterprise Manager</a> value add. All major IDE's (NetBeans, Eclipse, IntelliJ) have <a href="http://glassfishplugins.java.net/">plugins</a> to deploy to this version. GlassFish v2.1 update 3 is the latest version available for supported customers.

• <strong>GlassFish v3 Prelude</strong>: interesting if you want a lightweight Java EE 5 web container (no EJB, JMS, etc...) with admin tools. This is the first release using the modular OSGi architecture, IPS packaging format, and developer features such as <a href="http://blogs.oracle.com/jluehe/entry/retain_session_data_during_redeployment">preserve session across redeployments</a>. This was released in November 2008 and is a <a href="https://www.oracle.com/sun/index.html">supported product</a> (although not a long-lived as traditional software at Sun). It also offers native deployment of <a href="http://java.net/projects/glassfish-scripting/">Grails and Rails</a> applications. Some people use this version in development and deploy to v2.1.

• <strong>GlassFish v3 Preview</strong>: while not yet a supported product, this is a more recent version building on the same foundation as the above "Prelude" version, only it now offers both a Web distribution and a full Java EE 6 (Preview) distribution. It has a number of improvements over the "Prelude" version (IPS and updatetool for instance) and certainly much closer to a fully-featured application server. The final version should ship in September 2009 and offer a JavaEE 6, single-instance architecture. At that point this will become a supported product. The centralized administration will come in the v3.1 release which will mean feature parity with v2.1. If you like bleeding edge stuff, promoted builds for v3 are <a href="http://dlc.sun.com.edgesuite.net/glassfish/v3/promoted/">here</a>.

For more details on the releases, including sustaining (restricted) releases, please visit <a href="http://blogs.oracle.com/GlassFishForBusiness/">http://blogs.sun.com/GlassFishForBusiness/ </a>