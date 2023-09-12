---
id: 17145
title: '让Google赔了Oracle $88亿的9行代码 &#038; 37个包'
date: '2021-01-06T19:19:39+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/2021/01/06/17145'
permalink: '/?p=17145'
---

<!-- wp:image {"id":16548} -->
<figure class="wp-block-image"><img src="https://www.jayxu.com/log/wp-content/uploads/2018/05/Oracle-Google-Android-Lawsuit-1.jpg" alt="" class="wp-image-16548"/></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>9行代码</h2>
<!-- /wp:heading -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">private static void rangeCheck(int arrayLen, int fromIndex, int toIndex) {
    if (fromIndex > toIndex)
        throw new IllegalArgumentException("fromIndex(" + fromIndex +
             ") > toIndex(" + toIndex+")");
    if (fromIndex &lt; 0)
        throw new ArrayIndexOutOfBoundsException(fromIndex);
    if (toIndex > arrayLen)
        throw new ArrayIndexOutOfBoundsException(toIndex);
}
</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2>37个包</h2>
<!-- /wp:heading -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><p>java.awt.font</p><p>java.beans</p><p>java.io</p><p>java.lang</p><p>java.lang.annotation</p><p>java.lang.ref</p><p>java.lang.reflect</p><p>java.net</p><p>java.nio</p><p>java.nio.channels</p><p>java.nio.channels.spi</p><p>java.nio.charset</p><p>java.nio.charset.spi</p><p>java.security</p><p>java.security.acl</p><p>java.security.cert</p><p>java.security.interfaces</p><p>java.security.spec</p><p>java.sql</p><p>java.text</p><p>java.util</p><p>java.util.jar</p><p>java.util.logging</p><p>java.util.prefs</p><p>java.util.regex</p><p>java.util.zip</p><p>javax.crypto</p><p>javax.crypto.interfaces</p><p>javax.crypto.spec</p><p>javax.net</p><p>javax.net.ssl</p><p>javax.security.auth</p><p>javax.security.auth.callback</p><p>javax.security.auth.login</p><p>javax.security.auth.x500</p><p>javax.security.cert</p><p>javax.sql</p></blockquote>
<!-- /wp:quote -->