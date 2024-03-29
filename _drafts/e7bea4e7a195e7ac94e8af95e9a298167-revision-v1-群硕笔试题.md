---
id: 17490
title: 群硕笔试题
date: '2021-03-25T12:45:06+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/?p=17490'
permalink: '/?p=17490'
---

<!-- wp:paragraph -->
<p>群硕的笔试在语言方面主要是Java和C++，夹了一道C#题，趁记忆犹新的时候记下来 :!:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>一、给了一棵二叉树的前序遍历和中序遍历，要求写出后序遍历。<br>看一下数据结构就行了，很easy。提示：前序遍历的第一个节点为根结点，在中序遍历中根结点的左边节点是左子树，右边节点是右子树，如此递归。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>二、什么是物理内存和虚拟内存，OS中为什么要使用虚拟内存？<br>看OS的书。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>三、解释一下C#中的“<code data-enlighter-language="generic" class="EnlighterJSRAW">delegate</code>”。<br>原先不清楚的，然后在技术面试的时候问了一下面试官，原来类似于一个队列，队列中存的是函数指针（托管函数），运行时队列中的函数会在一个线程中被依次执行。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>四、与子程序传递参数有哪些方法？<br>汇编题，我想起来三个：参数压栈、参数存寄存器、参数存数据段。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>五、解释一下Java中的<code data-enlighter-language="generic" class="EnlighterJSRAW">String</code>和<code data-enlighter-language="generic" class="EnlighterJSRAW">StringBuffer</code>，什么时候需要使用<code data-enlighter-language="generic" class="EnlighterJSRAW">StringBuffer</code>？<br>核心是<code data-enlighter-language="generic" class="EnlighterJSRAW">String</code>对象是不变对象，连接、取子串等操作会生成新的对象，旧对象可能会被回收。<code data-enlighter-language="generic" class="EnlighterJSRAW">StringBuufer</code>则是可变对象，上述操作将在原对象上进行。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>六、Java中哪些容器的默认布局器（layout）是<code data-enlighter-language="generic" class="EnlighterJSRAW">BorderLayout</code>？<br>这个不是拿得很准，就写了<code data-enlighter-language="generic" class="EnlighterJSRAW">JFrame</code>及其子类，<code data-enlighter-language="generic" class="EnlighterJSRAW">Frame</code>及其子类。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>七、一个C++的函数：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"cpp"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="cpp" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">int operation(int numberA, int numberB){
    return numberA + numberB;
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>然后声明了三个变量：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"cpp"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="cpp" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">int a = 2;
int result1 = operation(5, a++);
int result2 = operation(5+a, ++a);</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>问<code data-enlighter-language="generic" class="EnlighterJSRAW">result1</code>和<code data-enlighter-language="generic" class="EnlighterJSRAW">result2</code>的值。<br>原先以为考的是传值、传引用的问题，结果仔细一看考得是a++和++a的问题，这就简单了。<br><code data-enlighter-language="generic" class="EnlighterJSRAW">result1 = 7, result2 = 12</code></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>八、如果父类的析构函数没有声明为虚函数的话在父类的指针上调用析构函数会有什么后果？<br>屏蔽多态，子类申请的资源将不被释放。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>九、定义了一个类：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"cpp"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="cpp" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class Something{
pulic:
    Something();
    void setValue(int val){
        value = val;
    }

private:
    int value;
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>以及一个函数：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"cpp"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="cpp" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">void doSomething(int val){
    Something* sth = new Something(); // Line 1
    sth-&amp;gt;setValue(val); // Line 2
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>问Line 2如果是<code data-enlighter-language="generic" class="EnlighterJSRAW">doSomething()</code>的最后一行的话会有什问题？<br><code data-enlighter-language="generic" class="EnlighterJSRAW">doSomething</code>执行完后<code data-enlighter-language="generic" class="EnlighterJSRAW">sth</code>没有被销毁，内存泄漏。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>十、写一个程序将输入的16进制转为10进制。<br>基础</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>十一、设计一个微波炉的控制程序（OO）。<br>这道题有点意思，我主要用<code data-enlighter-language="generic" class="EnlighterJSRAW">Observer</code>模式设计了一个定时器，然后把微波炉烹饪的对象抽象为<code data-enlighter-language="generic" class="EnlighterJSRAW">Cookable</code>。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>十二、逻辑题，一列火车以15 mph的速度从北京开往上海，另一列火车以20 mph的速度从上海开往北京，一只鸟（比较笨 ;) ）速度25 mph，在两列火车之间来回飞，相遇即折回。问到两列火车相遇这只笨鸟一共飞了多远？<br>很简单，因为鸟一直在飞，所以一共飞了<code><code data-enlighter-language="generic" class="EnlighterJSRAW">s/(15 + 20)</code></code>，s为上海到北京之间的距离，那么它一共飞了<code><code data-enlighter-language="generic" class="EnlighterJSRAW">s/(15 + 20) * 25</code></code> mile。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>12道题，除了那道C#题，其它觉得没多少地方能扣我分了，当天晚上就没睡好，很兴奋。果然第二天上午就打电话来让我去面试，效率真的很高，然后就果然顺利拿到了offer :cool:</p>
<!-- /wp:paragraph -->