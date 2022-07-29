---
id: 302
title: Synthetica破解
date: '2008-03-17T10:29:34+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/2008/03/17/302/'
permalink: /2008/03/17/302
aktt_notify_twitter:
    - 'yes'
    - 'yes'
dsq_thread_id:
    - '4271292234'
views:
    - '7561'
shorturl:
    - 'http://goo.gl/y7qxv'
duoshuo_thread_id:
    - '6.3356040351308E+18'
posturl_add_url:
    - 'yes'
---

话说前段时间提到把<a href="http://www.javasoft.de/synthetica/themes/" target="_blank">Synthetica</a>给破了，而网上关于破解的文章很少，所以今天就详细说说我是怎么破的。

<strong>准备知识</strong>

Synthetica是一套很漂亮的Java的look &amp; feel，大家可以去主页上跑一下demo（JWS的，需要安装JRE） 。可惜是commercial的，虽然有评估版下载，但是恶心的是，在评估版界面的最下方会有一块多余的区域（下图）

<a title="before.png" href="http://jayxu.com/log/wp-content/uploads/2008/03/before.png"><img src="http://jayxu.com/log/wp-content/uploads/2008/03/before.png" alt="before.png" /></a>

那这次破解的目的就是把这块区域给去了。

就我这几次破解来看，破解主要分以下几个步骤：
1. 反编译
2. 找关键代码（比如序列号校验算法）
3. 修改源代码
4. 编译打包

其中第1步是前提，在这点上Java的byte code的反编译是比较容易的了，因为毕竟是中间码，而且编译期采取的优化手段不多，反编译过来的基本就是源码。这里推荐<a href="http://jd.benow.ca/" target="_blank">DJ Compiler</a>，一个相当老牌的Java反编译器。值得注意的是并不是所有的byte code都能顺利反编译，有些Java程序会使用所谓的“混淆”技术对编译后的代码就行破坏，混淆器一般采用以下方法破坏代码：
1. 不可反编译。这点其实基本不可能
2. 反编译后代码不可读。这点相当恶心，混淆器会把类名、方法名、字段名替换成没有意义的名字，当你打开编辑器放眼望去全是“class A”，“int _fld00043”，“void _mhd2314”的时候你就知道该有多痛苦了
3. 插入不可编译代码。这一点也比较恶心，说穿了就是直接修改byte code中的指令，使用<span style="text-decoration: underline;">合法的，但不可能从源代码编译到的</span>指令替代原有的指令（比较拗口），比如使用“goto”替代循环。这样你的代码即使可以反编译成源代码但只能看不能改，除非你把goto再替换回去

这次Syn并没有使用混淆，所以用DJ很轻易地就反编了，接下来的活就是怎么找关键代码。一开始我以为评估版输入序列号校验成功后就升级成商业版，于是在那儿找了半天序列号的校验方法，没找到。后来凯子提供一条线索，Syn的商业版是要重新下的，于是猜测评估版和商业版不是一个版本（有时候破解也是要点推理的：-）），估计不会校验注册码。于是改变方向找加那一行字的代码，最后找到了：
<pre class="lang:java decode:1 " >public void paintBorder(Component component, Graphics g, int j, int k, int l, int i1){
    ...
    g.setColor(UIManager.getColor("Panel.background"));
    g.fillRect(j, i1, l, i1 + 16);
    g.setColor(new Color(0xcc0000));
    g.setFont(g.getFont().deriveFont(10F));
    g.drawString("Synthetica - Unregistered Evaluation Copy!", 0, k + i1 + g.getFontMetrics().getAscent());
    ...
}
</pre>
可以看出来它是通过Java 2D直接绘上去的，所以把这几句 注了，编译，打包，就ok了，最终结果：

<a title="after.png" href="http://jayxu.com/log/wp-content/uploads/2008/03/after.png"><img src="http://jayxu.com/log/wp-content/uploads/2008/03/after.png" alt="after.png" /></a>