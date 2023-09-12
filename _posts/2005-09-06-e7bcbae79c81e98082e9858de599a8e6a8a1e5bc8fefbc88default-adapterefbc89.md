---
id: 10214
title: '缺省适配器模式（Default Adapter）'
date: '2005-09-06T12:01:00+08:00'
author: Jay
layout: post
guid: 'http://www.blogjava.net/fidodido/archive/2005/09/06/12197.html'
permalink: /2005/09/06/10214
aktt_notify_twitter:
    - 'yes'
    - 'yes'
views:
    - '3650'
shorturl:
    - 'http://goo.gl/frO0r'
posturl_add_url:
    - 'yes'
duoshuo_thread_id:
    - '6.3356046835324E+18'
dsq_thread_id:
    - '4931936021'
---

<!-- wp:heading -->
<h2 class="wp-block-heading">一、概述</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>当不需要全部实现适配器接口提供的方法时，可先设计一个抽象类实现适配器接口，并为接口中每个方法提供一个默认实现（空方法）。那么该抽象类的子类可有选择地覆盖父类的某些方法来实现需求。</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">二、结构</h2>
<!-- /wp:heading -->

<!-- wp:image {"id":18310,"sizeSlug":"full","linkDestination":"attachment"} -->
<figure class="wp-block-image size-full"><a href="https://www.jayxu.com/2005/09/06/10214/defaultadapter"><img src="https://www.jayxu.com/log/wp-content/uploads/2023/03/defaultadapter.png" alt="" class="wp-image-18310"/></a></figure>
<!-- /wp:image -->

<!-- wp:heading -->
<h2 class="wp-block-heading">三、动机</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>对于一个接口不想使用其所有方法时</p>
<!-- /wp:paragraph -->