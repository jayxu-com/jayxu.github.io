---
id: 10324
title: 有关Character.isLetter()和Character.isLetterOrDigit()
date: '2010-12-10T11:27:40+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=10324'
permalink: /2010/12/10/10324
aktt_tweeted:
    - '1'
    - '1'
aktt_notify_twitter:
    - 'yes'
    - 'yes'
dsq_thread_id:
    - '4277804496'
views:
    - '12858'
shorturl:
    - 'http://goo.gl/2DfVf'
duoshuo_thread_id:
    - '6.3356047139201E+18'
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>在项目中有时候可能需要判断输入的是否全是英文或数字，如果你不善于使用正则，JDK中提供了<a href="http://download.oracle.com/javase/6/docs/api/java/lang/Character.html" target="_blank" rel="noopener noreferrer">Character</a>类对字符进行操作，其中的 <a href="http://download.oracle.com/javase/6/docs/api/java/lang/Character.html#isLetter(char)" target="_blank" rel="noopener noreferrer">isLetter</a>和<a href="http://download.oracle.com/javase/6/docs/api/java/lang/Character.html#isLetterOrDigit(char)" target="_blank" rel="noopener noreferrer">isLetterOrDigit</a>方法貌似可以做到这一点。但是如果你试下下面的代码，你会失望的：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">System.out.println(Character.isLetter('中'));</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>很不幸地，Java天生提供了对unicode的支持，因此在她眼里中文也是“letter”，所以上面打印出的是true……。替代方案是，使用<a href="http://commons.apache.org/" target="_blank" rel="noopener noreferrer">Apache Commons</a>子项目中的<a href="http://commons.apache.org/lang/" target="_blank" rel="noopener noreferrer">lang</a>库，<a href="http://commons.apache.org/proper/commons-lang/javadocs/api-release/org/apache/commons/lang3/CharUtils.html" target="_blank" rel="noopener noreferrer">CharUtils</a>的<a href="http://commons.apache.org/proper/commons-lang/javadocs/api-release/org/apache/commons/lang3/CharUtils.html#isAsciiAlpha(char)" target="_blank" rel="noopener noreferrer">isAsciiAlpha</a>和<a href="http://commons.apache.org/proper/commons-lang/javadocs/api-release/org/apache/commons/lang3/CharUtils.html#isAsciiAlphanumeric(char)" target="_blank" rel="noopener noreferrer">isAsciiAlphanumberic</a>可以帮助你只对英文字母进行判断</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>多说一句，commons项目是个大宝库，其中提供了大量对JDK的增强API，lang库就是对java.lang的增强，比如使用反射生成toString的<a href="http://commons.apache.org/proper/commons-lang/javadocs/api-release/org/apache/commons/lang3/builder/ToStringBuilder.html" target="_blank" rel="noopener noreferrer">ToStringBuilder</a>，使用反射生成hashCode的<a href="http://commons.apache.org/proper/commons-lang/javadocs/api-release/org/apache/commons/lang3/builder/HashCodeBuilder.html" target="_blank" rel="noopener noreferrer">HashCodeBuilder</a>，使用反射生成equals的<a href="http://commons.apache.org/proper/commons-lang/javadocs/api-release/org/apache/commons/lang3/builder/EqualsBuilder.html" target="_blank" rel="noopener noreferrer">EqualsBuilder</a>等等，大家可以慢慢自己发掘～</p>
<!-- /wp:paragraph -->