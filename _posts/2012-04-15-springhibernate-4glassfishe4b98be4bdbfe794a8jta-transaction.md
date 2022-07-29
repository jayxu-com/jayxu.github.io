---
id: 13435
title: 'Spring+Hibernate 4+Glassfish之使用JTA Transaction'
date: '2012-04-15T23:43:58+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13435'
permalink: /2012/04/15/13435
posturl_add_url:
    - 'yes'
views:
    - '11312'
duoshuo_thread_id:
    - '6.3356049899599E+18'
dsq_thread_id:
    - '4271399810'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>今天下午开始尝试将项目的transaction交给Glassfish的JTA管理，因为之后会使用到JMS，需要与JDBC组成跨data source的事务。但是不知道是没人这么干过还是大家不屑于将完整的配置过程就下来，JBoss的官方文档、Spring的官方文档、SOF都没有可用的配置建议。经过差不多半天时间的Google和尝试，终于配置成功，在此分享</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>环境：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Spring 3.1.1</li><li>Hibernate 4.1.1</li><li>Glassfish 3.1.2</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>应该都是最新的版本，Spring配置文件如下：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"xml","highlight":"7,8"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="xml" data-enlighter-theme="" data-enlighter-highlight="7,8" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">...
&lt;!-- 打开Spring的@Transaction声明式事务支持 -->
&lt;!-- 配置Spring使用JTA事务 -->

...

    hibernate.current_session_context_class = jta&lt;!-- 1 -->
    hibernate.transaction.manager_lookup_class = org.hibernate.transaction.SunONETransactionManagerLookup&lt;!-- 2 -->
	
...</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>关键配置在1和2处：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>根据Hibernate官方文档<a href="http://docs.jboss.org/hibernate/orm/4.1/manual/en-US/html_single/#transactions-demarcation-jta" target="_blank" rel="noopener noreferrer">此处</a>和<a href="http://docs.jboss.org/hibernate/orm/4.1/manual/en-US/html_single/#architecture-current-session" target="_blank" rel="noopener noreferrer">此处</a>的描述：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>When configuring Hibernate's transaction factory, choose</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>org.hibernate.transaction.JTATransactionFactory</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>if you use JTA directly (BMT), and </p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>org.hibernate.transaction.CMTTransactionFactory</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>in a CMT session bean. Remember to also set </p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>hibernate.transaction.manager_lookup_class</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>Ensure that your </p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>hibernate.current_session_context_class</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>is either unset (backwards compatibility), or is set to </p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>"jta"</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>See the Javadocs for the&nbsp;</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>org.hibernate.context.spi.CurrentSessionContext</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>interface for a detailed discussion of its contract. It defines a single method, </p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre class="wp-block-preformatted"><code>currentSession()</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>by which the implementation is responsible for tracking the current contextual session. Out-of-the-box, Hibernate comes with three implementations of this interface:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>org.hibernate.context.internal.JTASessionContext: current sessions are tracked and scoped by a&nbsp;JTAtransaction. The processing here is exactly the same as in the older JTA-only approach. See the Javadocs for details.</li><li>org.hibernate.context.internal.ThreadLocalSessionContext:current sessions are tracked by thread of execution. See the Javadocs for details.</li><li>org.hibernate.context.internal.ManagedSessionContext: current sessions are tracked by thread of execution. However, you are responsible to bind and unbind a&nbsp;Session&nbsp;instance with static methods on this class: it does not open, flush, or close a&nbsp;Session</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>即需要设置</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>hibernate.current_session_context_class</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>为jta，同时设置</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>hibernate.transaction.manager_lookup_class</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>但是这里耽误了我半天的就是</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>hibernate.transaction.manager_lookup_class</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>的设置，这里只说“需要设置”，但是没有给出具体的值，虽然<a href="http://docs.jboss.org/hibernate/orm/4.1/manual/en-US/html_single/#configuration-optional-transactionstrategy" target="_blank" rel="noopener noreferrer">文档</a>中给出了一个</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>TransactionManagerLookup</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>接口的实现类列表，但是其中没有Glassfish⋯⋯</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>又经过了N久的Google，在<a href="http://www.ibm.com/developerworks/forums/thread.jspa?messageID=14024638" target="_blank" rel="noopener noreferrer">这里</a>和<a href="http://forum.springsource.org/showthread.php?100914-Glassfish-v3-0-1-JTA-(JPA2-Hibernate3-5)-Spring-3-exception-mapping" target="_blank" rel="noopener noreferrer">这里</a>找到了一个神奇的实现类：</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>org.hibernate.transaction.SunONETransactionManagerLookup</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>根据<a rel="noopener noreferrer" href="http://docs.jboss.org/hibernate/orm/3.6/javadocs/org/hibernate/transaction/SunONETransactionManagerLookup.html" target="_blank">Javadoc</a>，此类实现了“for Sun ONE Application Server 7 and above”的查找策略，想想GF的前身即是Sun AS，应该可以使用。试了一下，终于work~</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>这里遗留的一个问题是，我并没有在Hibernate 4.1.1的源代码里找到org.hibernate.transaction.SunONETransactionManagerLookup（上面的Javadoc也是3.6的Javadoc），甚至整个org.hibernate.transaction包下面只有TransactionManagerLookup接口的定义。因此究竟是怎么work的我没有找到最终答案，如果有人知道，希望可以在这里留下答案</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2012-4-16补：今天启动服务器时偶然间发现抛出个warning，</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>hibernate.transaction.manager_lookup_class</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>在Hibernate 4中已被deprecated掉，需要使用</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">hibernate.transaction.jta.platform=org.hibernate.service.jta.platform.internal.SunOneJtaPlatform</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>替换</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2012-4-17补：今天发现Hibernate的自动flush失效，查看GF启动日志后发现一个新的warning：</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>JTASessionContext being used with JDBCTransactionFactory; auto-flush will not operate correctly with getCurrentSession()</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>查文档后发现上面的1、2处需要指定TransactionFactory，否则Hibernate将默认使用JDBCTransactionFactory：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">hibernate.transaction.factory_class=org.hibernate.transaction.JTATransactionFactory</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>问题解决。这次的经验同样是，虽然app server启动时一般会输出大量log，但是要让自己养成从中发现warning级别及以上信息的洞察力，这样解决问题将事半功倍</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2012-4-22补：今天又遇到了问题，在使用Query.iterate()方法时，Hibernate抛出异常：</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>org.hibernate.HibernateException: proxy handle is no longer valid</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>根据<a href="https://forum.hibernate.org/viewtopic.php?p=2453582" target="_blank" rel="noopener noreferrer">这里</a>的讨论，把</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>JTATransactionFactory</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>换成了</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted {"className":"inline:true decode:1"} -->
<pre class="wp-block-preformatted inline:true decode:1"><code>CMTTransactionFactory</code></pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>问题解决：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">hibernate.transaction.factory_class=org.hibernate.transaction.CMTTransactionFactory
</pre>
<!-- /wp:enlighter/codeblock -->