---
id: 17614
title: Alloy破解过程
date: '2021-05-11T00:43:21+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/?p=17614'
permalink: '/?p=17614'
---

<!-- wp:enlighter/codeblock {"language":"java"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="java" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">package com.incors.plaf.alloy;
 
import java.io.*;
import java.util.GregorianCalendar;
import java.util.zip.CRC32;
import java.util.*;

public class ch{
  public ch(){
  }

  private static void a(){
    if(a)
      return;
    bi.a("alloy.licenseCode",cr()); // feed serial automatically
    String s=bi.a("alloy.licenseCode");
    if(s == null)
      try{
        InputStream inputstream=(com.incors.plaf.alloy.ch.class).getClassLoader().
                                getResourceAsStream("alloylnf.lic");
        if(inputstream != null){
          InputStreamReader inputstreamreader=new InputStreamReader(inputstream,
                                              "ISO-8859-1");
          BufferedReader bufferedreader=new BufferedReader(inputstreamreader);
          s=bufferedreader.readLine();
          System.out.println(s);
          bi.a("alloy.licenseCode",s);
          bufferedreader.close();
          inputstream.close();
        }
      }
      catch(Exception exception){}
    if(s != null){
      int l=s.indexOf('#');
      int i1=s.indexOf('#',l + 1);
      int j1=s.indexOf('#',i1 + 1);
      f=s.substring(0,l);
      if(f.length() &amp;gt; 1)
        j=a(f);
      e=s.substring(l + 1,i1);
      d=s.substring(0,i1);
      g=Long.parseLong(s.substring(i1 + 1,j1),36);
      h=Long.parseLong(s.substring(j1 + 1),36);
      b();
    }
    a=true;
  }

  private static void b(){
    i.update((h % 127L + d).getBytes());
    if(i.getValue() != g){
      b=false;
      return;
    }
    if(j != null &amp;amp;&amp;amp; (new GregorianCalendar()).after(j)){ // 试用号过期
      b=false;
      return;
    }
    b=true;
    if(j != null &amp;amp;&amp;amp; (new GregorianCalendar()).after(new GregorianCalendar(2003,7,12))){ // 如果使用期大于1年
      GregorianCalendar gregoriancalendar=new GregorianCalendar();
      gregoriancalendar.add(1,1);
      if(j.after(gregoriancalendar)){
        c=false;
        return;
      }
    }
    c=true;
  }

  private static GregorianCalendar a(String s){
    int l=Integer.parseInt(s.substring(0,4));
    int i1=Integer.parseInt(s.substring(5,7));
    int j1=Integer.parseInt(s.substring(8,10));
    return new GregorianCalendar(l,i1 - 1,j1 + 1);
  }

  public static boolean c(){
    if(!a)
      a();
    return bi.a("alloy.licenseCode") != null;
  }

  public static boolean d(){
    if(!a)
      a();
    return b;
  }

  public static boolean e(){
    if(!a)
      a();
    return c;
  }

  private static boolean a=false;
  private static boolean b=false;
  private static boolean c=false;
  private static String d;
  public static String e;
  public static String f;
  public static long g=0L;
  public static long h=0L;
  private static CRC32 i=new CRC32();
  public static GregorianCalendar j;

  private static String cr(){ // 自动生成序列号，比当前时间晚一个月
    Calendar cal=new GregorianCalendar();
    cal.add(cal.MONTH,1);

   String s="";
    int year=cal.get(cal.YEAR);
    int month=cal.get(cal.MONTH);
    int day=cal.get(cal.DAY_OF_MONTH);

    s+=year + "/" + (month &amp;lt; 10 ? "0" + month : month) + "/" + (day &amp;lt; 10 ? "0" + day : day);
    s+="#oop@vip.163.com#128cw93#1a193l";

    int l=s.indexOf('#');
    int i1=s.indexOf('#',l + 1);
    int j1=s.indexOf('#',i1 + 1);

    String e=s.substring(l + 1,i1);
    String d=s.substring(0,i1);
    String sg=s.substring(i1 + 1,j1);
    Long g=Long.parseLong(sg,36);
    Long h=Long.parseLong(s.substring(j1 + 1),36);

    CRC32 crc=new CRC32();
    crc.update((h % 127L + d).getBytes());
    Long ii=crc.getValue();
    StringBuffer sn=new StringBuffer(s).replace(i1 + 1,j1,Long.toString(ii,36));
    return sn.toString();
  }
}
</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>关键代码处有注释，我就详细讲一下<code><code data-enlighter-language="generic" class="EnlighterJSRAW">cr()</code></code>。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>由于Alloy的序列号的时间比当前时间晚一年以上也视作invalid，因此我在<code><code data-enlighter-language="generic" class="EnlighterJSRAW">cr()</code></code>中动态生成一个序列号，该序列号比当前时间晚一个月，使用<code><code data-enlighter-language="generic" class="EnlighterJSRAW">bi.a()</code></code>注入程序中（15行）。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>行到132行是具体的算号过程，可见“<code><code data-enlighter-language="generic" class="EnlighterJSRAW">128cw93</code></code>”和“<code><code data-enlighter-language="generic" class="EnlighterJSRAW">1a1931</code></code>”其实是两个36进制的数。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>第132行把算得的校验值替换117行生成的字符串中的相应位置上的字符串，生成新的序列号。</p>
<!-- /wp:paragraph -->