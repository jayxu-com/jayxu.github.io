---
id: 13237
title: '有关Java泛型的类型擦除（type erasing）'
date: '2012-02-02T17:24:41+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13237'
permalink: /2012/02/02/13237
posturl_add_url:
    - 'yes'
views:
    - '6857'
duoshuo_thread_id:
    - '6.3356049354549E+18'
dsq_thread_id:
    - '4276190915'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>自从Java 5引入泛型之后，Java与C++对于泛型不同的实现的优劣便一直是饭后的谈资。在我之前的很多training中，当讲到Java泛型时总是会和C++的实现比较，一般得出的结论是</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Java使用类型擦除（type erasing），泛型信息只在编译时供javac作类型检查用，在编译后便被javac擦除，因此无法被反射</li><li>C++使用代码模板实现泛型，即在预处理时会生成类似｢list_int｣，｢list_char｣等的泛型类，虽然解决Java的运行时伪泛型的问题，但是会导致编译后的代码呈线性增长</li><li>于是在一般情况下，Java的类型擦除实现较优</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>这三条已经比绝大多数的Java培训讲师讲得深刻了。但是如果下面有人问｢在什么情况下C++的实现方式较优｣时，除了无法被反射，我很难现抓一个有说服力的例子。今天，Spring的RestTemplate终于给了我这个例子</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>我遇到的问题如下（阅读需要有一些Spring MVC、REST基础）</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>有一个返回类型为List的MVC方法：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">@RequestMapping(value = "...", method = RequestMethod.GET)
@ResponseBody
public List doSomethingREST() {
    List domainObjs = ... ;
    return domainObjs;
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>在运行时，Spring MVC会将List转换成JSON字符串并返回至客户端。但是如果我在另一个service中使用RestTemplate直接调用该REST接口，问题便来了：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">List domainObjs = this.restTemplate.getForObject(this.restURL, List.class);</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>关键在于第二个参数，是返回值的类型，RestTemplate会根据此类型选择适当的MessageConverter将调用REST接口的返回值反序列化为与类型匹配的对象。由于List的泛型参数在编译时被擦除，于是RestTemplate便无法确定List中的内容。｢一般情况下｣（REST接口返回值不是List类型）不会有问题，但是巧合的是，如果服务器端使用JSON对REST结果进行序列化，返回值会被封装在List中，此时，Spring已无法判断开发人员是想直接获得List封装的JSON内容还是需要更进一步使用Jackson库将JSON反序列化为Java对象。现实情况下，Spring选择的前者，于是便会抛出ClassCastException</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>上网搜了一圈，已经有人向Spring提交了enhancement请求（<a href="https://jira.springsource.org/browse/SPR-7002" target="_blank" rel="noopener noreferrer">这里</a>和<a href="https://jira.springsource.org/browse/SPR-7023" target="_blank" rel="noopener noreferrer">这里</a>，其中第一个链接中的walkaround可以work），但是目前没有milestone</p>
<!-- /wp:paragraph -->