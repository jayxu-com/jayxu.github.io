---
id: 1284
title: java.util.StringTokenization
date: '2004-12-27T15:53:00+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/2004/12/27/1284/'
permalink: /2004/12/27/1284
aktt_notify_twitter:
    - 'no'
    - 'no'
views:
    - '2947'
shorturl:
    - 'http://goo.gl/1xjyR'
duoshuo_thread_id:
    - '6.3356042742774E+18'
dsq_thread_id:
    - '4446395998'
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>今天室友老七做数据库大作业，其中要实现一个功能，就是输入一个以“,”分隔的数字串，将得到的数字填入一个数组，他自己写了一个，很笨拙。我提议他用java.util.StringTokenization类。那个类使用起来很方便：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">StringTokenizer st = new StringTokenizer("this is a test"," ");
while (st.hasMoreTokens()) {
    System.out.println(st.nextToken());
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>输出：</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>this<br>is<br>a<br>test</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>（构造器中第二个字符串是分隔符的集合，默认是空格）</p>
<!-- /wp:paragraph -->