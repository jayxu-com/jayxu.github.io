---
id: 16028
title: java.util.Calendar中的陷阱
date: '2005-10-24T17:23:45+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=16028'
permalink: /2005/10/24/16028
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '2062'
dsq_thread_id:
    - '5295404748'
---

需求：
从输入框得到用户分开输入的年、月、日，将信息做为Date类型插入数据库

解决一：
<pre lang="java" class="">InputBean bean = new InputBean(); // 封装用户输入

// 获取用户输入，封装于bean对象中

Calendar cal = Calendar.getInstance();
cal.set(cal.YEAR,bean.getYear()); // Year
cal.set(cal.MONTH,bean.getMonth()); // Month
cal.set(cal.DAY_OF_MONTH,bean.getDay()); // Day

// 数据库操作</pre>
陷阱：
Calendar中的MONTH字段和数组下标一样，从0开始，0代表Calendar.JANUARY，1代表Calendar.FEBUARY……12代表次年Calendar.JANUARY。因此用户输入的月份在置入Calendar对象之前必须进行处理，即减一。

解决二：
<pre lang="java">InputBean bean = new InputBean(); // 封装用户输入

// 获取用户输入，封装于bean对象中

Calendar cal = Calendar.getInstance();
cal.set(cal.YEAR,bean.getYear()); // Year
cal.set(cal.MONTH,bean.getMonth() - 1); // Month
cal.set(cal.DAY_OF_MONTH,bean.getDay()); // Day

// 数据库操作</pre>