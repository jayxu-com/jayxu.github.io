---
id: 17488
title: 位图（bitmap）排序
date: '2021-03-25T12:40:37+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/?p=17488'
permalink: '/?p=17488'
---

<!-- wp:paragraph -->
<p>放假之前从图书馆借来《编程珠玑》，开篇遍把我震住，作者以位图排序优雅地解决了一个现实问题：<br>有3000万个没有重复的电话号码，1M内存，外存比较充裕，需要将这3000万个电话排序</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>借此作者引出了位图排序：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>位图排序是指以一个N位长的串，每位上以“1”或“0”表示需要排序的集合（后简称“集合”）中的数。比如集合为<code><code data-enlighter-language="generic" class="EnlighterJSRAW">{2,7,4,9,1,10}</code></code>，则生成一个10位的串，将第2、7、4、9、1、10位置为“<code data-enlighter-language="generic" class="EnlighterJSRAW">1</code>”，其余位置为“<code data-enlighter-language="generic" class="EnlighterJSRAW">0</code>”，这样当把串中所有位都置完后，排序也自动完成了（因为串的下标是有序的）：<code><code data-enlighter-language="generic" class="EnlighterJSRAW">1101001011</code></code></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>位图排序的代码如下（重写于2021.3.25）：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"java"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="java" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">public static int[] bitmapSort(int[] set) {
    var max = Arrays.stream(set).max().getAsInt();
    var array = new int[max + 1];
    var ret = new int[set.length];

    for (int i : set) {
        array[i] = 1;
    }

    for (int i = 0, j = 0; i &lt; array.length; i++) {
        if (array[i] == 1) {
            ret[j++] = i;
        }
    }

    return ret;
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>可以看出，位图排序的时间复杂度是<code><code data-enlighter-language="generic" class="EnlighterJSRAW">O(n)</code></code>的，比一般的排序都快，但它是以空间换时间（需要一个N位的串），而且有一些限制，比如排序前集合大小最好已知，而且集合中元素的最大重复次数必须已知，最好是稠集数据（不然空间浪费很大）。</p>
<!-- /wp:paragraph -->