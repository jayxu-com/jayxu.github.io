---
id: 10218
title: 使用策略模式（Strategy）实现多关键字排序
date: '2005-08-04T12:37:00+08:00'
author: Jay
layout: post
guid: 'http://www.blogjava.net/fidodido/archive/2005/08/04/9181.html'
permalink: /2005/08/04/10218
aktt_notify_twitter:
    - 'yes'
    - 'yes'
views:
    - '3461'
dsq_thread_id:
    - '4271400062'
shorturl:
    - 'http://goo.gl/t9v9R'
duoshuo_thread_id:
    - '6.3356046837044E+18'
posturl_add_url:
    - 'yes'
---

<p>｢策略模式｣的出现，是为了提供一套相互之间可灵活替换的算法，在不影响上层接口的情况下，用户可以自由选择不同的算法完成逻辑。策略模式的UML示意图如下：</p>
<p><a class="hoverZoomLink" href="http://www.jayxu.com/log/wp-content/uploads/2005/08/r_image0021.jpg"><img alt="" class="alignnone size-medium wp-image-10222 hoverZoomLink" height="210" src="http://www.jayxu.com/log/wp-content/uploads/2005/08/r_image002.jpg" width="480" /></a></p>
<p>其中算法的模型接口在｢抽象策略｣中定义，各具象策略实现不同的策略。｢消费API｣就是调用不同算法的类，在其内部根据不同需要选择不同的算法。有时需要将具象策略实例化后再传给其它类，这时可以使用｢简单工厂｣（Simple Factory）或｢工厂方法｣（Factory Method）生成所需的具象策略。下面就以我正在做的一个项目，简化一下后说明一下策略模式的使用。 该项目是一个小型的商业网站，逻辑层由Servlet实现。用户有一个需求，需要从数据库调出商品信息后能够对记录按名称（name）、规格（standard）、价格（price）和注册日期（register date）进行排序。虽然可以考虑按不同的排序关键字使用不同的sql语句（即不同的order by）查询数据库。但这样做的网络数据流量太大，每次需要从数据库完整地取回一个数据集（ResultSet），所以我选择了将数据集一次取到客户端的一个List中，然后在客户端按不同的关键字对List进行排序。 java.util.Collections类中有一个public static void sort(List list, Comparator comparator)的方法，可以按照不同的Comparator对象对list进行排序，它使用的是快速排序，所以效率非常高。而java.util.Comparator是一个接口：</p>
<pre class="lang:java decode:1 " >package java.util;

public abstract interface Comparator {
    boolean equals(Object object);

    int compare(Object object, Object object1);
}</pre>
<p>其中和排序有关的是compare方法，它返回一个整数，若第一个参数比第二个参数｢大｣，则返回一个正数，若｢小｣则返回一个负数，若｢相等｣则返回0，这里的｢大｣、｢小｣、｢相等｣是由compare方法具体实现定义的一种比较标准。由这个方法不禁想到C语言中qsort函数中使用的函数指针int *compare(*,*)，JAVA中之所以没有函数指针，就是用接口取代了（更详细的介绍见《Effective Java》中第22条｢用类和接口来代替函数指针｣）。 很明显，Comparator接口就是我们的｢抽象策略｣，sort方法就是我们的｢消费API｣，而不同的｢具象策略｣就是我们从Comparator接口实现的根据不同关键字排序的类。 整个排序模型的UML图如下，其中为了作图方便，我从Comparator继承了一个接口ItemComparator，根据不同的关键字从ItemComparator接口泛化了NameComparator类，PriceComparator类，RegisterDateComparator类和StandardComparator类。实际运用中不需要这个接口，四个类可以直接从Comparator泛化。ItemBean是一个封装了商品信息的bean，List中存放的就是这些bean。ItemSort和ItemComparator以及四个具体类实现了｢简单工厂｣模式，并封装了sort方法。</p>
<p><a class="hoverZoomLink" href="http://www.jayxu.com/log/wp-content/uploads/2005/08/o_strategy.dfPackage1.jpg"><img alt="" class="alignnone size-medium wp-image-10221 hoverZoomLink" height="480" src="http://www.jayxu.com/log/wp-content/uploads/2005/08/o_strategy.dfPackage.jpg" width="427" /></a></p>
<p>下面是具体的代码（StandardComparator类的代码与NameComparator类的代码大同小异，在这里不列出）：</p>
<p>NameComparator类</p>
<pre class="lang:java decode:1 " >package com.lim.designpatterns.strategy;

public class NameComparator implements ItemComparator{
    NameComparator(){} // 将构造器封装，包外的类欲得到Comparator实例只能通过简单工厂

    public int compare(Object o1,Object o2){
        String name1=((ItemBean)o1).getName();
        String name2=((ItemBean)o2).getName();

        return name1.compareTo(name2); // 调用String的CompareTo方法
    }
}</pre>
<p>PriceComparator类</p>
<pre class="lang:java decode:1 " >package com.lim.designpatterns.strategy;

public class PriceComparator implements ItemComparator{
    PriceComparator(){}

    public int compare(Object o1,Object o2){
        Double price1=new Double(((ItemBean)o1).getPrice());
        Double price2=new Double(((ItemBean)o2).getPrice());

        return price1.compareTo(price2); // 调用Double的CompareTo方法
    }
}</pre>
<p>RegisterDateComparator类</p>
<pre class="lang:java decode:1 " >package com.lim.designpatterns.strategy;

import java.util.*;

public class RegisterDateComparator implements ItemComparator{
    RegisterDateComparator(){}

    public int compare(Object o1,Object o2){
        Date date1=((ItemBean)o1).getRegisterDate();
        Date date2=((ItemBean)o2).getRegisterDate();

        return date1.compareTo(date2); // 调用Date的CompareTo方法
    }
}</pre>
<p>ItemSort类</p>
<pre class="lang:java decode:1 " >package com.lim.designpatterns.strategy;

import java.util.*;

public class ItemSort{
    public static List sort(List items,ItemComparator c){
        Collections.sort(items,c);
        return items;
    }

    public static final ItemComparator NAME=new NameComparator(); // 简单工厂

    public static final ItemComparator PRICE=new PriceComparator();

    public static final ItemComparator STANDARD=new StandardComparator();

    public static final ItemComparator REG_DATE=new RegisterDateComparator();
}</pre>
<p>TestItemSort类</p>
<pre class="lang:java decode:1 " >package com.lim.designpatterns.strategy;

import java.util.*;

public class TestItemSort{
    public static void main(String[] args){
        List items=new ArrayList();
        // 向List添加条目

        items=ItemSort.sort(items,ItemSort.NAME); // 按名称排序

        items=ItemSort.sort(items,ItemSort.PRICE); // 按价格排序

        items=ItemSort.sort(items,ItemSort.REG_DATE); // 按注册日期排序

        items=ItemSort.sort(items,ItemSort.STANDARD); // 按规格排序
    }
}</pre>
