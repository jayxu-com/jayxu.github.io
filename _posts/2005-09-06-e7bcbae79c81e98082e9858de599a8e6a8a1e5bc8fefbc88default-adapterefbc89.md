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
    - '3467'
shorturl:
    - 'http://goo.gl/frO0r'
posturl_add_url:
    - 'yes'
duoshuo_thread_id:
    - '6.3356046835324E+18'
dsq_thread_id:
    - '4931936021'
---

<h2>一、概述</h2>
当不需要全部实现适配器接口提供的方法时，可先设计一个抽象类实现适配器接口，并为接口中每个方法提供一个默认实现（空方法）。那么该抽象类的子类可有选择地覆盖父类的某些方法来实现需求。
<h2>二、结构</h2>
<img src="http://images.blogjava.net/blogjava_net/fidodido/2507/defaultadapter.png" alt="defaultadapter.png" width="138" height="243" border="0" />
<h2>三、动机</h2>
对于一个接口不想使用其所有方法时