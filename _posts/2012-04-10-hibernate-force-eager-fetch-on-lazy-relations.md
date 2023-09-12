---
id: 13414
title: '[Hibernate] Force Eager Fetch on Lazy Relations'
date: '2012-04-10T20:27:11+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13414'
permalink: /2012/04/10/13414
posturl_add_url:
    - 'yes'
views:
    - '4334'
duoshuo_thread_id:
    - '6.3356049896033E+18'
dsq_thread_id:
    - '4415876253'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">Outter outter = session.createQuery("...").uniqueResult();
Hibernate.initialize(outter.getInners());</pre>
<!-- /wp:enlighter/codeblock -->