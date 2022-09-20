---
id: 2342
title: 'Spring之Hibernate+JBoss Treecache实现Hibernate集群'
date: '2010-06-09T14:53:28+08:00'
author: Jay
layout: post
guid: 'http://jayxu.com/?p=2342'
permalink: /2010/06/09/2342
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
views:
    - '6822'
shorturl:
    - 'http://goo.gl/RXRk4'
posturl_add_url:
    - 'yes'
duoshuo_thread_id:
    - '6.3356046086347E+18'
dsq_thread_id:
    - '4288463182'
---

<strong><em>本文版权归本人所有，任何转载请标明出处</em></strong>

Hibernate作为一个ORM框架可以说已经做到了极致，但是绝大多数情况下Hibernate都被应用于单容器环境中，以至于互联网上能够找到的在集群环境中使用的参考少之又少，和Spring整合的就更别说了。实际上，Hibernate可以使用JBoss的Treecache作为二级缓存以支持分布式集群

本文将使用Spring 3.0.2框架集成Hibernate 3.5.2，并将<a href="http://jbosscache.jboss.org/" target="_blank">Treecache</a> 3.2.5作为二级缓存

Spring配置
<pre lang="xml">
<context:annotation-config />

<bean id="sessionFactory" class="org.springframework.orm.hibernate3.annotation.AnnotationSessionFactoryBean">
        ...
        <property name="hibernateProperties">
            <value>
                hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
                hibernate.cache.use_second_level_cache=true
                hibernate.show_sql=true
                hibernate.cache.region.factory_class=org.hibernate.cache.jbc2.SharedJBossCacheRegionFactory
                hibernate.cache.use_query_cache=true
                hibernate.hbm2ddl.auto=update
            </value>
        </property>
    </bean>
</pre>

其中第1行打开Spring的annotation支持，即使用annotation替代之前版本中的大量XML配置（貌似这个选项在Spring 2.5中就被引入，但不知道是因为大家懒还是配置文件的基本内容都是在互联网上Ctrl C+V 2.5之前的代码，反正互联网上一搜Spring的配置满眼都是XML片段）；第8行打开二级缓存；第10行选择Treecache作为缓存region工厂的实现类

对于需要被缓存的实体，只需要在类定义上加上@Cache注释，如：
<pre lang="java">
@Cache(usage = CacheConcurrencyStrategy.TRANSACTIONAL)
public class MyModel {
    ...
}
</pre>

由于Treecache只支持只读缓存和事务缓存，因此这里usage只能设为READ_ONLY或TRANSACTIONAL，但需要注意的是设为只读缓存时不能打开Hibernate的query cache

最后是Treecache的配置，如果配置文件名是treecache.xml且在classpath中则无需指定，否则需要在上述Spring配置的代码段中指定。至于具体配置内容，可参考Treecache源代码中的sample，调优方式可参考Treecache文档，这里给一个sample
<pre lang="xml">
<?xml version="1.0" encoding="UTF-8"?>
<jbosscache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="urn:jboss:jbosscache-core:config:3.2">

   <!-- Configure the TransactionManager -->
   <transaction transactionManagerLookupClass="org.jboss.cache.transaction.GenericTransactionManagerLookup"/>

   <clustering mode="replication">
      <!--
       timeout: The max amount of time (in milliseconds) we wait until the
             state (i.e. the contents of the cache) are retrieved from
             existing members in a clustered environment
      -->
      <stateRetrieval timeout="20000"/>

      <!-- JGroups protocol stack properties. -->
      <jgroupsConfig>
         <udp discard_incompatible_packets="true" enable_bundling="true" enable_diagnostics="false" ip_ttl="2"
              loopback="false" max_bundle_size="64000" max_bundle_timeout="30" mcast_addr="224.12.12.12"
              mcast_port="45588" mcast_recv_buf_size="100000000" mcast_send_buf_size="640000"
              oob_thread_pool.enabled="true" oob_thread_pool.keep_alive_time="10000" oob_thread_pool.max_threads="20"
              oob_thread_pool.min_threads="8" oob_thread_pool.queue_enabled="false" oob_thread_pool.queue_max_size="10"
              oob_thread_pool.rejection_policy="Run" thread_naming_pattern="pl" thread_pool.enabled="true"
              thread_pool.keep_alive_time="10000" thread_pool.max_threads="15" thread_pool.min_threads="8"
              thread_pool.queue_enabled="true" thread_pool.queue_max_size="100000"
              thread_pool.rejection_policy="Discard"
              tos="8" ucast_recv_buf_size="20000000" ucast_send_buf_size="640000" use_concurrent_stack="true"
              use_incoming_packet_handler="true"/>
         <ping num_initial_members="3" timeout="2000"/>
         <merge2 max_interval="30000" min_interval="10000"/>
         <fd_SOCK/>
         <fd max_tries="5" shun="true" timeout="10000"/>
         <verify_SUSPECT timeout="1500"/>
         <pbcast.NAKACK discard_delivered_msgs="true" gc_lag="0" retransmit_timeout="300,600,1200,2400,4800"
                        use_mcast_xmit="true"/>
         <unicast timeout="300,600,1200,2400,3600"/>
         <pbcast.STABLE desired_avg_gossip="50000" max_bytes="400000" stability_delay="1000"/>
         <pbcast.GMS join_timeout="5000" print_local_addr="true" shun="false" view_ack_collection_timeout="5000"
                     view_bundling="true"/>
         <fc max_credits="500000" min_threshold="0.2"/>
         <frag2 frag_size="60000"/>
         <pbcast.STREAMING_STATE_TRANSFER/>
         <pbcast.FLUSH timeout="0"/>
      </jgroupsConfig>

      <async />
      <!-- Alternatively, to use sync replication, comment out the element above and uncomment the element below.  -->
      <!-- <sync /> -->

   </clustering>
</jbosscache>
</pre>

需要注意的是第7行，集群mode。Treecache的分布式同步有两种模式：replication和invalidation。这两者的区别是：对于replication，每一个节点（缓存）中的对象改变时，该节点会将新对象通过多播的方式告知多播组中的其它节点，其它节点自行更新；而对于invalidation模式，发生改变的节点只通知其它节点某对象已发生改变，其它节点直接将自己缓存中的该对象标记为invalid，待下次需要使用时通过数据库更新该对象。这样一解释就能发现取舍的策略了：若网络比数据库金贵，选择invalidation，标记自己的对象，让数据库忙活去吧；若数据库金贵，使用replication多播对象

另外，由于Treecache使用了基于多播协议的jgroup库作为底层通信框架，在配置Treecache集群时不需要了解多播组中其他节点IP，只需要把第19行的多播地址（必须是D类地址）配成一个的就行了，jgroup会自行发现多播组中的其它节点

<h3>世界杯大酬宾：如何使用JMX监控Treecache的状态</h3>
启动容器；打开任意JMX客户端，如jconsole；在进程列表中选择容器的java进程并连接；选择“mbean”标签，找到“jboss.cache”节点，如下图

<a href="http://www.jayxu.com/log/wp-content/uploads/2010/06/VisualVM-1.3.png"><img src="http://www.jayxu.com/log/wp-content/uploads/2010/06/VisualVM-1.3-400x235.png" alt="" title="VisualVM 1.3" width="400" height="235" /></a>
在这个节点下可以看到所有Treecache通过JMX暴露的属性，包括命中率、缓存对象等