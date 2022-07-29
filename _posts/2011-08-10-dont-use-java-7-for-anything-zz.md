---
id: 11629
title: 'Don&#8217;t Use Java 7, For Anything [zz]'
date: '2011-08-10T16:08:36+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=11629'
permalink: /2011/08/10/11629
aktt_notify_twitter:
    - 'yes'
views:
    - '4906'
aktt_tweeted:
    - '1'
shorturl:
    - 'http://goo.gl/6KHlw'
duoshuo_thread_id:
    - '6.3356048552598E+18'
dsq_thread_id:
    - '4289851619'
---

<p>From <a href="http://www.lucidimagination.com/blog/2011/07/28/dont-use-java-7-for-anything/" target="_blank">here</a>. Shit happens, Oracle wanna risk the fame of Java?!</p>
<p>&nbsp;</p>
<p>Java 7 GA was <a href="http://mail.openjdk.java.net/pipermail/announce/2011-July/000106.html">released today</a>, but as noted by Uwe Schindler, there are some very frightening bugs in HotSpot Loop optimizations that are enabled by default. In the best case scenario, these bugs cause the JVM to crash. In the worst case scenario, they cause incorrect execution of loops.</p>
<p>Bottom Line: <a href="http://www.lucidimagination.com/search/document/1a0d3986e48a9348/warning_index_corruption_and_crashes_in_apache_lucene_core_apache_solr_with_java_7">Don&rsquo;t use Java 7</a> for anything (unless maybe you know you don&rsquo;t have any loops in your java code)</p>
<p><em>From: Uwe Schindler<br />
	Date: Thu, 28 Jul 2011 23:13:36 +0200<br />
	Subject: [WARNING] Index corruption and crashes in Apache Lucene Core / Apache Solr with Java 7</em></p>
<p><em>Hello Apache Lucene &amp; Apache Solr users,<br />
	Hello users of other Java-based Apache projects,</em></p>
<p><em>Oracle released Java 7 today. Unfortunately it contains hotspot compiler<br />
	optimizations, which miscompile some loops. This can affect code of several<br />
	Apache projects. Sometimes JVMs only crash, but in several cases, results<br />
	calculated can be incorrect, leading to bugs in applications (see Hotspot<br />
	bugs 7070134 [1], 7044738 [2], 7068051 [3]).</em></p>
<p><em>Apache Lucene Core and Apache Solr are two Apache projects, which are<br />
	affected by these bugs, namely all versions released until today. Solr users<br />
	with the default configuration will have Java crashing with SIGSEGV as soon<br />
	as they start to index documents, as one affected part is the well-known<br />
	Porter stemmer (see LUCENE-3335 [4]). Other loops in Lucene may be<br />
	miscompiled, too, leading to index corruption (especially on Lucene trunk<br />
	with pulsing codec; other loops may be affected, too &ndash; LUCENE-3346 [5]).</em></p>
<p><em>These problems were detected only 5 days before the official Java 7 release,<br />
	so Oracle had no time to fix those bugs, affecting also many more<br />
	applications. In response to our questions, they proposed to include the<br />
	fixes into service release u2 (eventually into service release u1, see [6]).<br />
	This means you cannot use Apache Lucene/Solr with Java 7 releases before<br />
	Update 2! If you do, please don&rsquo;t open bug reports, it is not the<br />
	committers&rsquo; fault! At least disable loop optimizations using the<br />
	-XX:-UseLoopPredicate JVM option to not risk index corruptions.</em></p>
<p><em>Please note: Also Java 6 users are affected, if they use one of those JVM<br />
	options, which are not enabled by default: -XX:+OptimizeStringConcat or<br />
	-XX:+AggressiveOpts</em></p>
<p><em>It is strongly recommended not to use any hotspot optimization switches in<br />
	any Java version without extensive testing!</em></p>
<p><em>In case you upgrade to Java 7, remember that you may have to reindex, as the<br />
	unicode version shipped with Java 7 changed and tokenization behaves<br />
	differently (e.g. lowercasing). For more information, read<br />
	JRE_VERSION_MIGRATION.txt in your distribution package!</em></p>
<p><em>On behalf of the Lucene project,<br />
	Uwe</em></p>
<p><em>[1] http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=7070134<br />
	[2] http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=7044738<br />
	[3] http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=7068051<br />
	[4] https://issues.apache.org/jira/browse/LUCENE-3335<br />
	[5] https://issues.apache.org/jira/browse/LUCENE-3346<br />
	[6] http://s.apache.org/StQ</em></p>
