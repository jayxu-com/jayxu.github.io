---
id: 15523
title: 原型模式（Prototype）
date: '2005-04-12T00:30:56+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=15523'
permalink: /2005/04/12/15523
posturl_add_url:
    - 'yes'
views:
    - '2385'
dsq_thread_id:
    - '4931932816'
duoshuo_thread_id:
    - '6.3356053623134E+18'
---

<h2>一、概述</h2>
原型模式属于对象创建模式，通过给出一个原型对象来指明所要创建的对象类型，然后用复制这个对象的方法创建出更多同类型的对象。
<h2>二、结构</h2>
<h3>1、简单形式</h3>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_prototype1.gif"><img class="alignnone size-full wp-image-15524" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_prototype1.gif" alt="o_prototype1" width="314" height="168" /></a>

Client：提出创建对象的请求

Prototype：抽象角色，给出所有具体原型类所需的接口

ConcretePrototype：被复制的对象
<h3>2、登记形式</h3>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_prototype2.gif"><img class="alignnone size-full wp-image-15525" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_prototype2.gif" alt="o_prototype2" width="326" height="227" /></a>

PrototypeManager：创建并记录具体对象
<h2>三、浅克隆与深克隆</h2>
浅克隆：仅做refrence一级的克隆，refrence所指的对象不被克隆

深克隆：将refrence所指的对象进行递归克隆，需考虑克隆深度及循环克隆问题
<h2>四、动机</h2>
替换较复杂的等级结构的工厂方法
<h2>五、优缺点</h2>
<ol>
 	<li>允许动态地增加或减少产品类，且对整个现有的产品结构没有影响</li>
 	<li>提供简化的创建结构</li>
 	<li>具有动态加载新功能的能力</li>
 	<li>产品类不需要有确定的等级结构</li>
 	<li>每一个类必须配备一个克隆方法</li>
</ol>