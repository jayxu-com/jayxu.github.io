---
id: 13131
title: '使用Spring LDAP ODM操作LDAP'
date: '2011-12-14T23:10:16+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13131'
permalink: /2011/12/14/13131
views:
    - '10019'
posturl_add_url:
    - 'yes'
duoshuo_thread_id:
    - '6.3356049345825E+18'
dsq_thread_id:
    - '4293133931'
---

Spring Source真的是个很神奇的开源社区，从《J2EE without EJB》开始为大家所知晓，到把IoC、AOP大范围地带到大家的开发模型中，再到和Hibernate、Struts组成每个Java函授学校必教的“SSH”组合，从此绿遍大江南北……

在国内，大马路上随便抓一个Java程序员，10个里有9个半知道Spring；有9个知道怎么把SSH“组装”到一起（是的，“组装”，和流水线上的蓝领熟练工没有本质区别）；有9个半知道IoC、AOP；有2个知道IoC和AOP的本质；有3个知道Spring其实分为core、context、orm、tx等不同子框架；有1个知道Spring 3之后可以用annotation取代之前版本大部分的xml配置；有2个知道Spring mvc和security；有半个知道其实Spring的子框架远不止这些……这就是我们当前Java码农们的实际情况。而造成这一局面的，我谓之三害——高校计算机系功利的培养模式、以北大青鸟为首的各种速成班的祸害和程序员们自己懒惰、人云亦云、拒绝思考的慢性自杀

牢骚发完，本文将通过介绍Spring的两个子框架：Spring LDAP和Spring LDAP ODM，来实现对LDAP的操作

项目主页：<a href="http://www.springsource.org/ldap" target="_blank">http://www.springsource.org/ldap</a>，该框架通过提供和ORM中相似的机制对LDAP相关操作进行封装，主要包括：
<ul>
	<li>类比SessionFactory的LdapContextSource</li>
	<li>类比HibernateTemplate等的LdapTemplate</li>
	<li>伪事务支持，能否与tx框架的TransactionManager混用未知</li>
	<li>类比JPA的使用@Entry、@Attribute、@Id标注的ODM——Object Directory Mapping</li>
</ul>
本文（原先）目标：使用ODM将User类与LDAP中的实体进行映射，LDAP中的实体的objectClass包括inetOrgPerson，organizationalPerson，person，shadowAccount和top

相关配置文件、代码在<a href="http://static.springsource.org/spring-ldap/docs/1.3.x/reference/html/" target="_blank">http://static.springsource.org/spring-ldap/docs/1.3.x/reference/html/</a>上已经很详细了，这里只是做一点旁注，全部来自于这几天和Spring LDAP的斗智斗勇
<ul>
	<li>对于shadowAccount的shadowLastChange域，值是一个整形，至于具体含义网上没有找到解释，试了几次之后发现是从1970-1-1 00:00:00至今的天数，如果model里定义的是Date类型的话，需要自行实现org.springframework.ldap.odm.typeconversion.impl.Converter接口进行转换</li>
	<li>对于@Entry标记，其中的objectClasses定义必须与objectClass完全一致。在新建和查询object时，ODM会根据此标记进行匹配，无需再指定objectClass</li>
	<li>每个entry必须指定@Id字段，类型为javax.naming.Name，其实就是DN。但是若在LdapContextSource中指定了base，则DN将会按照base截取相对路径。比如，DN为cn=user,ou=users,dc=jayxu,dc=com，base为dc=jayxu,dc=com，则取出的user对象DN为cn=user,ou=users</li>
	<li>如果使用Spring MVC对LDAP对象进行JSON序列化，必须注意javax.naming.Name中的某些字段无法被序列化，所以在转换成JSON之前需要将DN置null。一种方法是使用@JsonIgnoreProperties标记model类，比如：@JsonIgnoreProperties("dn")</li>
	<li>对于不需要与LDAP进行映射的字段使用@Transient进行标记</li>
	<li>考虑使用org.springframework.ldap.pool.factory.PoolingContextSource引入连接池</li>
	<li>如果事务中需要与JDBC进行互操作，需要使用org.springframework.ldap.transaction.compensating.manager.ContextSourceAndDataSourceTransactionManager作为tx manager</li>
</ul>

2012-04-17更新：有关LDAP事务的具体配置，可参考<a href="http://www.jayxu.com/2012/04/17/13449/" target="_blank">这里</a>