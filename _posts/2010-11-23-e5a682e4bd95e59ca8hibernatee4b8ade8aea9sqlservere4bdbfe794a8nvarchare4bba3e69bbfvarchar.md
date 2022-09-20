---
id: 10275
title: 如何在Hibernate中让SQLServer使用nvarchar代替varchar
date: '2010-11-23T16:19:38+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=10275'
permalink: /2010/11/23/10275
aktt_tweeted:
    - '1'
    - '1'
aktt_notify_twitter:
    - 'yes'
    - 'yes'
dsq_thread_id:
    - '4307518253'
views:
    - '8462'
shorturl:
    - 'http://goo.gl/mFcLm'
duoshuo_thread_id:
    - '6.3356047137272E+18'
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>有关SQLServer中varchar和nvarchar的区别可以直接去google。一般在中文系统中应该使用nvarchar作为字符串的对应类型，但是Hibernate中的默认实现SQLServerDialect使用了varchar。以下方法可以简单地转为使用nvarchar：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>自己写一个dialect，继承SQLServerDialect，在构造器中将原先varchar类型的注册声明覆盖：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">registerColumnType(Types.VARCHAR, "nvarchar($l)");</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>千万注意，“$”后面的是字段长度的占位符，是“l(ength)”，而不是数字“1”（因为看hibernate的doc时没分清“l”和“1”，浪费了我一上午去找原因）</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>然后在hibernate的配置文件中将hibernate.dialect的值设为你的dialect实现类就OK了</p>
<!-- /wp:paragraph -->