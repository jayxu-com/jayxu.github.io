---
id: 13449
title: 'Spring LDAP Transaction &#8211; Unofficial yet Working Config Manual'
date: '2012-04-17T01:45:54+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13449'
permalink: /2012/04/17/13449
posturl_add_url:
    - 'yes'
views:
    - '10301'
duoshuo_thread_id:
    - '6.3356049903667E+18'
dsq_thread_id:
    - '4285073556'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>之前的<a href="http://www.jayxu.com/2011/12/14/13131" target="_blank" rel="noopener noreferrer">一篇文章</a>介绍了Spring的LDAP子项目和ODM框架，其中提到了LDAP事务，但没有深入，而且那个配置中的事务也是不work的。上个周末在和JTA斗智斗勇的同时把项目中的LDAP事务也搞定了，现在可以做到将LDAP和Hibernate的session factory放在同一个事务上下文中进行ACID管理，即LDAP和数据库操作实现“all or none”（虽然是伪事务，具体下文会提到）。当然，对于Spring LDAP事务配置官方和Google上同样没有任何可参考或操作的文档说明，不然我也不用连着两个晚上码字造福大众了。另外，为了造福资本主义国家的程序猿们，同时向他们展示社会主义国家的制度优越性，以下将切换至英文</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Spring LDAP is a amazing framework esp. for its LdapTemplate and ODM, providing a&nbsp;consistent&nbsp;point of view of developing LDAP code with the well-known and document-friendly techniques - JdbcTemplate and ORM. Unfortunately, Spring LDAP is not that widely-used, for its sluggish development progress (1.3.1 so far) and lacking of document/samples. This post will focus on a even rare yet important topic of Spring LDAP - transaction. For other information like O-D mapping or LDAP context source, pls refer to the <a href="http://docs.spring.io/spring-ldap/site/reference/html/" target="_blank" rel="noopener noreferrer">official document</a>, and some tips <a href="http://www.jayxu.com/2011/12/14/13131" target="_blank" rel="noopener noreferrer">here</a> if you can read Chinese.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Environment</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Spring LDAP 1.3.1</li><li>Spring * 3.1.1</li><li>Hibernate 4.1.1</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>Goal</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>Implement a method annotated with @Transactional, which&nbsp;demonstrates&nbsp;a business service</li><li>The service invokes two persist DAOs, one uses Hibernate's session factory and the other uses Spring's ODM</li><li>The two persist actions should follow "all or none" rule, that is, if JDBC action fails after LDAP action, LDAP action should rollback, vice versa</li></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2>IMPORTANT</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>As described in the <a href="http://static.springsource.org/spring-ldap/site/reference/html/transactions.html" target="_blank" rel="noopener noreferrer">official document</a>, TX in Spring LDAP is "not real"</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>it should be noted that the provided support is all client side. The wrapped transaction is not an XA transaction. No two-phase as such commit is performed, as the LDAP server will be unable to vote on its outcome. Once again, however, for the majority of cases the supplied support will be sufficient.</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>Show time!</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>Spring configuration</h2>
<!-- /wp:heading -->

<!-- wp:enlighter/codeblock {"language":"xml"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="xml" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">&lt;bean id="contextSourceTarget" class="org.springframework.ldap.core.support.LdapContextSource">
	&lt;property name="url" value="..." />
	&lt;property name="base" value="dc=jayxu,dc=com" />
	&lt;property name="userDn" value="cn=admin,dc=jayxu,dc=com" />
	&lt;property name="password" value="..." />
&lt;/bean>

&lt;bean id="pooledContextSource" class="org.springframework.ldap.pool.factory.PoolingContextSource">
	&lt;property name="contextSource" ref="contextSourceTarget" />
	&lt;property name="testOnBorrow" value="true" />
	&lt;property name="dirContextValidator" ref="dirContextValidator" />
&lt;/bean>

&lt;bean id="dirContextValidator" class="org.springframework.ldap.pool.validation.DefaultDirContextValidator" />

&lt;bean class="org.springframework.ldap.core.LdapTemplate">
	&lt;property name="contextSource" ref="contextSource" />
&lt;/bean>

&lt;bean id="contextSource" class="org.springframework.ldap.transaction.compensating.manager.TransactionAwareContextSourceProxy">
	&lt;constructor -arg ref="pooledContextSource" />
&lt;/bean>

&lt;bean id="ldapTransactionManager" class="com.jayxu.common.ldap.ContextSourceAndHibernate4TransactionManager">
	&lt;property name="contextSource" ref="contextSource" />
	&lt;property name="sessionFactory" ref="sessionFactory" />
&lt;/bean>

&lt;bean id="odmManager" class="org.springframework.ldap.odm.core.impl.OdmManagerImplFactoryBean">
	&lt;property name="contextSource" ref="contextSource" />
	&lt;property name="managedClasses">
		&lt;set>
			&lt;value>...&lt;/value>
		&lt;/set>
	&lt;/property>
	...
&lt;/bean>

&lt;bean class="org.springframework.transaction.interceptor.TransactionProxyFactoryBean">
	&lt;property name="transactionManager" ref="ldapTransactionManager" />
	&lt;property name="target" ref="myService" />
	&lt;property name="transactionAttributes">
		&lt;props>
			&lt;prop key="*">PROPAGATION_REQUIRES_NEW&lt;/prop>
		&lt;/props>
	&lt;/property>
&lt;/bean>
&lt;bean id="myService" class="com.jayxu.service.MyService" />

&lt;tx:annotation-driven /></pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:image {"id":13468,"linkDestination":"custom"} -->
<figure class="wp-block-image"><a href="http://www.jayxu.com/log/wp-content/uploads/2012/04/Resource-thread_common_src_main_resources_spring-ldap.xml-Eclipse-_Users_ijay_workspace.png"><img src="https://www.jayxu.com/log/wp-content/uploads/2012/04/Resource-thread_common_src_main_resources_spring-ldap.xml-Eclipse-_Users_ijay_workspace.png" alt="" class="wp-image-13468"/></a></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>This diagram gives a overview of the beans' references<br>
<br>
In your service class, you should annotate your transactional methods or the whole class with</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">@Transactional(value = "ldapTransactionManager")</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>here "value" refers to the tx manager name above. My test code looks like</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">@Transactional(value = "ldapTransactionManager")
public void ldapTx() {
	odm.create(...);
	sessionFactory.getCurrentSession().persist(...);

	throw new RuntimeException();
}
</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>then config logger level of org.springframework.ldap and org.springframework.transaction to DEBUG, if everything works well, you can find something in the output like</p>
<!-- /wp:paragraph -->

<!-- wp:shortcode -->
[raw]
[DEBUG] org.springframework.ldap.transaction.compensating.LdapCompensatingTransactionOperationFactory:59 - Bind operation recorded
[DEBUG] org.springframework.ldap.transaction.compensating.BindOperationExecutor:97 - Performing bind operation
[DEBUG] org.springframework.transaction.support.TransactionSynchronizationManager:140 - Retrieved value [org.springframework.ldap.transaction.compensating.manager.DirContextHolder@3ed024df] for key [org.springframework.ldap.pool.factory.PoolingContextSource@165b3858] bound to thread [main]
[DEBUG] org.springframework.ldap.transaction.compensating.manager.TransactionAwareDirContextInvocationHandler:120 - Leaving transactional context open
[DEBUG] org.springframework.transaction.support.TransactionSynchronizationManager:140 - Retrieved value [org.springframework.orm.hibernate4.SessionHolder@55661f7b] for key [org.hibernate.internal.SessionFactoryImpl@7fb5438d] bound to thread [main]
[DEBUG] org.springframework.transaction.interceptor.TransactionInterceptor:406 - Completing transaction for [com.jayxu.service.UserLdapService.addUserTx] after exception: java.lang.RuntimeException
[DEBUG] org.springframework.transaction.interceptor.RuleBasedTransactionAttribute:130 - Applying rules to determine whether transaction should rollback on java.lang.RuntimeException
[DEBUG] org.springframework.transaction.interceptor.RuleBasedTransactionAttribute:147 - Winning rollback rule is: null
[DEBUG] org.springframework.transaction.interceptor.RuleBasedTransactionAttribute:152 - No relevant rollback rule found: applying default rules
[DEBUG] org.springframework.transaction.compensating.support.DefaultCompensatingTransactionOperationManager:79 - Performing rollback
[DEBUG] org.springframework.transaction.support.TransactionSynchronizationManager:331 - Clearing transaction synchronization
[DEBUG] org.springframework.transaction.support.TransactionSynchronizationManager:243 - Removed value [org.springframework.orm.hibernate4.SessionHolder@55661f7b] for key [org.hibernate.internal.SessionFactoryImpl@7fb5438d] from thread [main]
[DEBUG] org.springframework.transaction.support.TransactionSynchronizationManager:243 - Removed value [org.springframework.jdbc.datasource.ConnectionHolder@22013e9b] for key [org.springframework.jdbc.datasource.DriverManagerDataSource@c20e54a] from thread [main]
[DEBUG] org.springframework.transaction.compensating.support.AbstractCompensatingTransactionManagerDelegate:121 - Cleaning stored transaction synchronization
[DEBUG] org.springframework.transaction.support.TransactionSynchronizationManager:243 - Removed value [org.springframework.ldap.transaction.compensating.manager.DirContextHolder@3ed024df] for key [org.springframework.ldap.pool.factory.PoolingContextSource@165b3858] from thread [main]
[DEBUG] org.springframework.ldap.transaction.compensating.manager.ContextSourceTransactionManagerDelegate:103 - Closing target context
[/raw]
<!-- /wp:shortcode -->

<!-- wp:paragraph -->
<p>Line 1 indicates save point being created while line 10 indicates the rollback</p>
<!-- /wp:paragraph -->