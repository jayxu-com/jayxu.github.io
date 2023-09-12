---
id: 2401
title: 误区！double类型做加减法不会有误差？
date: '2010-08-25T10:36:08+08:00'
author: Jay
layout: post
guid: 'http://jayxu.com/?p=2401'
permalink: /2010/08/25/2401
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
dsq_thread_id:
    - '4279938646'
views:
    - '8456'
shorturl:
    - 'http://goo.gl/h4O5b'
duoshuo_thread_id:
    - '6.3356046330959E+18'
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>如果你跟我一样以为Java的double类型只有在作乘除法时才会出现误差，那试一下在Java里执行一下下面的代码：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">public static void  main(String[] args) {
    System.out.println(44.42 + 710.79 + 44.42 +  88.85);
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>执行前先猜一下结果，是会输出888.48么？还是……？</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>建议：对于和钱有关的计算，不论加减乘除，统一使用 BigDecimal！</p></blockquote>
<!-- /wp:quote -->

<!-- wp:paragraph -->
<p>然而不多久之后同事告诉我另一个BigDecimal的问题，试一下下面的代码：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">System.out.println(new BigDecimal(0.99).setScale(2, RoundingMode.DOWN).toString());</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>结果是令人发指的0.98！</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>看了一下 BigDecimal(double)的源码，其中使用位操作分别提取了0.99浮点值的整数部分和纯小数部分，或者说是2的正数次幂和负数次幂部分。而这样提取出来的值纯小数部分本身就是近似的，与直接使用double类型没有本质区别，这是浮点表示法决定的，再经过2位截取后就产生了误差</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>而当使用BigDecimal(String)的构造器时得到的是精确值，因为该构造器将数字使用科学计数法表示，即 0.99表示为99*10^-2，这样做运算时先对齐至相同的整数位再进行计算</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>因此，对上面的补充是：如果要获取最精确的结果，请使用BD+字符串类型的构造器</p></blockquote>
<!-- /wp:quote -->