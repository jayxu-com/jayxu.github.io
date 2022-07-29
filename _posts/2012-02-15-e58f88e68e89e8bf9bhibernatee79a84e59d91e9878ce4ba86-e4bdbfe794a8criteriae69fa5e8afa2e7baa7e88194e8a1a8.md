---
id: 13263
title: 又掉进Hibernate的坑里了——使用Criteria查询级联表
date: '2012-02-15T04:09:43+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13263'
permalink: /2012/02/15/13263
posturl_add_url:
    - 'yes'
views:
    - '6441'
duoshuo_thread_id:
    - '6.335604961468E+18'
dsq_thread_id:
    - '4314366679'
---

Hibernate的dot-based级联表查询HQL可以算是能够大大提高生产力的特性之一，比如

User (1) ---- (1) City

一般会在User对象中维护一个City对象，然后使用以下方式进行查询：

<pre lang="java">sessionFactory.createQuery("from User where city.name=?").setString(0, "Shanghai")</pre>

但是上面的思路在今天使用Criteria时出现了问题，一直报错找不到属性"city.name"。经过再三google，原来是使用Criteria时需要自己维护级联关系，即

<pre lang="java">Criteria userCriteria = sessionFactory.createCriteria(User.class);
Criteria cityCriteria = userCriteria.createCriteria("city").add(Restrictions.eq("name", "Shanghai");</pre>

这个问题搞了一晚上，坑爹啊～