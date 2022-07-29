---
id: 15499
title: 'Mini Java编译器（六）'
date: '2005-03-16T12:05:10+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=15499'
permalink: /2005/03/16/15499
posturl_add_url:
    - 'yes'
views:
    - '1693'
dsq_thread_id:
    - '4930086206'
duoshuo_thread_id:
    - '6.3356053329197E+18'
---

<h2>七、系统工作过程及运行说明</h2>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_sequence.gif"><img src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_sequence.gif" alt="o_sequence" width="416" height="539" /></a>
&nbsp;
<h2>八、实例程序运行结果</h2>
<h3>示例一</h3>
<h4>代码</h4>
<pre class="lang:java decode:1 " >
class Main{
  public static void main(String[] args){
    System.out.println(10);
  }
}

class G{
  public int get(int num){
    int a;
    a=2;

    return a+5;
  }
}

class H extends G{
  int i;
  boolean bol;

  public int put(){
    i=1+2;
    i=12-3;
    i=2*7;

    bol=true &amp;&amp; false;
    bol=1&lt;2;

    return 10;
  }
}</pre>

<h4>继承树</h4>
<h4><a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_tree1.gif"><img src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_tree1.gif" alt="o_tree1" width="256" height="246" /></a></h4>
&nbsp;
<h4>符号表</h4>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_token1.gif"><img class="alignnone size-full wp-image-15503" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_token1.gif" alt="o_token1" width="536" height="226" /></a>
&nbsp;
<h4>内存分配表</h4>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_memory1.gif"><img class="alignnone size-full wp-image-15500" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_memory1.gif" alt="o_memory1" width="445" height="207" /></a>
&nbsp;
<h3>示例二</h3>
<h4>代码</h4>
<pre class="lang:java decode:1 " >
class Factorial {
    public static void main(String[] a) {
        System.out.println(new Fac().ComputeFac(10));
    }
}

class Fac extends Factorial{
    Fac f;
    Factorial ff;
    int i;

    public int ComputeFac(int num) {
      int numaux;
      if (num &lt; 1)
        numaux = 1;
      else
        numaux = num * (this.ComputeFac(num-1));

      return numaux;
    }
}

class F extends Fac{
}

class G extends Factorial{
}

class H{}

class I extends H{}

class J extends I{}

class GG extends I{}

class DD extends I{}
</pre>
&nbsp;
<h4>继承树</h4>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_tree2.gif"><img class="alignnone size-full wp-image-15506" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_tree2.gif" alt="o_tree2" width="221" height="256" /></a>
&nbsp;
<h4>符号表</h4>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_token2.gif"><img class="alignnone size-full wp-image-15504" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_token2.gif" alt="o_token2" width="501" height="410" /></a>
&nbsp;
<h4>内存分配表</h4>
<a href="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_memory2.gif"><img class="alignnone size-full wp-image-15501" src="http://www.jayxu.com/log/wp-content/uploads/2016/06/o_memory2.gif" alt="o_memory2" width="400" height="295" /></a>