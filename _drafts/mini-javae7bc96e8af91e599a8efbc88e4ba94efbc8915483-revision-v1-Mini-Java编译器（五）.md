---
id: 17280
title: 'Mini Java编译器（五）'
date: '2021-01-27T01:28:34+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/2021/01/27/17280'
permalink: '/?p=17280'
---

<h2>六、系统的设计和实现</h2>
这个编译器是用<span lang="EN-US">Java</span>写的，基于<span lang="EN-US">OO</span>技术，所以整个系统是尽量用<span lang="EN-US">OOD</span>设计的。<span lang="EN-US">OOD</span>中最小的设计粒度是类，本系统的大致类结构如下

&nbsp;
<h3><span lang="EN-US">compiler</span>包</h3>
整个系统的根，<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_compiler.gif"><img class="alignnone wp-image-15487 size-medium" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_compiler-600x753.gif" alt="o_compiler" width="600" height="753" /></a>

&nbsp;
<h3><span lang="EN-US">token</span>包</h3>
封装了所有的可识别单词，采用一符一码，单词对应的码定义在<span lang="EN-US">Token</span>类中，该类是抽象类，仅作继承用。该包<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_token.gif"><img class="alignnone size-medium wp-image-15491" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_token-600x1074.gif" alt="o_token" width="600" height="1074" /></a>

&nbsp;
<h3><span lang="EN-US">common</span>包</h3>
公用包，封装了一些公用的对象和数据结构：

<span lang="EN-US">HierarchyTree</span>类和<span lang="EN-US">HierarchyTreeNode</span>类定义了继承树结构；

<span lang="EN-US">MemoryTable</span>类和<span lang="EN-US">MemoryCell</span>类定义了需要内存分配表；

<span lang="EN-US">Locatable</span>接口和<span lang="EN-US">Locator</span>类定义了定位器；

<span lang="EN-US">TokenTable</span>定义了符号表；

&nbsp;
<h4>继承树（<span lang="EN-US">HierarchyTreeNode</span>和<span lang="EN-US">HierarchyTree</span>）</h4>
封装类之间的继承属性，数据机构上使用一棵<span lang="EN-US">N</span>叉双向树，可以由父节点直接访问子节点，也可以由子节点直接访问父节点。

<span lang="EN-US">Java</span>不支持多继承，<span lang="EN-US">Mini Java</span>连接口继承（<span lang="EN-US">implements</span>）也不支持，所以每个子节点只有一个父节点，而一个父节点可以有<span lang="EN-US">N</span>个子节点。

虽然<span lang="EN-US">Mini Java</span>规范中没有明确定义，但实现上仿照<span lang="EN-US">Java</span>将<span lang="EN-US">Object</span>类作为继承树的根节点。

具体实现时定义了一棵“伪树”，即存储结构为表，但以附加的<span lang="EN-US">level</span>属性区分父节点与叶结点。

<span lang="EN-US">HierarchyTreeNode</span>封装了节点，<span lang="EN-US">HierarchyTree</span>则封装了和树有关的一些操作（插入、查找）。

&nbsp;
<h4>符号表（<span lang="EN-US">TokenTable</span>和<span lang="EN-US">Identifier</span>）</h4>
因为只有以下几种情况会出现“标识符已定义”、“类已定义”或“方法已定义”语法错误：

同一个文件中声明了相同名称的类

同一个类中声明了相同名称的方法

同一个类中声明了相同名称的类变量

同一个方法中声明了相同名称的变量

方法中声明了与方法参数名称相同的变量

因此我在实现时修改了符号表的内容，去掉了“<span lang="EN-US">level</span>”属性，增加了“<span lang="EN-US">belongsTo</span>”属性，具体定义见第三部分的<span lang="EN-US">id_belongsTo</span>表。

<span lang="EN-US">common</span>包的<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_common.gif"><img class="alignnone size-medium wp-image-15486" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_common-600x602.gif" alt="o_common" width="600" height="602" /></a>

&nbsp;
<h3><span lang="EN-US">automation</span>包</h3>
封装了词法分析器和语法分析器，<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_automation.gif"><img class="alignnone size-full wp-image-15484" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_automation.gif" alt="o_automation" width="461" height="1241" /></a>

&nbsp;
<h3><span lang="EN-US">exception</span>包</h3>
封装了所有可抛出的异常，<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_exception.gif"><img class="alignnone size-medium wp-image-15488" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_exception-600x349.gif" alt="o_exception" width="600" height="349" /></a>

&nbsp;
<h3><span lang="EN-US">identifier</span>包</h3>
封装了所有标识符类别，实现<span lang="EN-US">Typable</span>接口的类具有类型属性，<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_identifier.gif"><img class="alignnone size-full wp-image-15489" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_identifier.gif" alt="o_identifier" width="510" height="696" /></a>

&nbsp;
<h3><span lang="EN-US">type</span>包</h3>
封装了所有类型，在<span lang="EN-US">Type</span>抽象类中提供<span lang="EN-US">factory()</span>方法，使用简单工厂（<span lang="EN-US">Simple Factory</span>）模式生成类型对象，<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_type.gif"><img class="alignnone size-medium wp-image-15492" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_type-600x282.gif" alt="o_type" width="600" height="282" /></a>

&nbsp;
<h3><span lang="EN-US">ui</span>包</h3>
封装用户界面

&nbsp;
<h4><span lang="EN-US">ClassTreeModel</span></h4>
继承自<span lang="EN-US">javax.swing.tree.TreeModel</span>，可将继承树的内容显示在图形界面中

&nbsp;
<h4>TokenTableModel</h4>
继承自<span lang="EN-US">javax.swing.table.AbstractTableModel</span>，可符号表的内容显示在图形界面中

&nbsp;
<h4>MemoryTableModel</h4>
继承自<span lang="EN-US">javax.swing.table.AbstractTableModel</span>，可内存分配表的内容显示在图形界面中

<span lang="EN-US">UML</span>图如下：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_ui.gif"><img class="alignnone size-medium wp-image-15494" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_ui-600x369.gif" alt="o_ui" width="600" height="369" /></a>