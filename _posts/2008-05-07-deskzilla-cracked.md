---
id: 352
title: 'Deskzilla Cracked'
date: '2008-05-07T00:32:20+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/?p=352'
permalink: /2008/05/07/352
dsq_thread_id:
    - '4271295567'
views:
    - '5839'
aktt_notify_twitter:
    - 'yes'
shorturl:
    - 'http://goo.gl/RaoUu'
duoshuo_thread_id:
    - '6.3356040902859E+18'
posturl_add_url:
    - 'yes'
---

最近破解上瘾了，昨天干到3点多，今天又花了一中午把<a href="http://almworks.com/deskzilla/overview.html" target="_blank">deskzilla</a>，一个bugzilla的桌面客户端）破解了。

<a href="http://www.jayxu.com/log/wp-content/uploads/2008/05/crack.png"><img class="alignnone size-full wp-image-353" title="crack" src="http://www.jayxu.com/log/wp-content/uploads/2008/05/crack.png" alt="" width="403" height="236" /></a>

这次破解花了很长时间，一是因为代码编译后被混淆了，找关键代码的时候着实花了不少时间。另一方面这个软件的license验证不是使用常见的布尔判断，而是用异常。这意味着必须仔细研究方法的调用栈，于是这次用了一个比较偷巧的方法：在代码中抛出并捕捉异常。在Java中，无论在代码何处抛出异常，JVM都会生成一个从程序入口到抛出异常方法的调用栈，这个机制在需要调用关系的场合非常有用，比如log4j，就是使用这种机制记录log的方法、行数、类名等等信息的。但是，这种机制是非常消耗资源的，因为调用栈里的每一个element都记录着方法、类、甚至行数（如果编译时打开“debug”开关）等信息，而这些信息都是通过反射机制从class文件里直接获得的。

通过对一堆类似huv、dww、dtg、gjt的混淆后的类的分析，终于找出了几个关键类：
<pre class="lang:java decode:1 " >
package z;

public class dza extends hwn {

    // ...

    static  {
        l = epv.a("Application.License.FULL", "Single-user license");
        m = epv.a("Application.License.EVAL", "Evaluation license");
        n = epv.a("Application.License.EAP", "EAP license");
        o = epv.a("Application.License.OS", "License for open-source projects");
        p = epv.a("Application.License.INVALID", "License is INVALID");
        r = epv.a("Application.License.FLOATING", "Floating license");
        s = epv.a("Application.License.PERSONAL", "Personal license");
        t = epv.a("Application.License.ACADEMIC", "Academic license");
        u = epv.a("Application.License.SITE", "Site license");
        a = new dza("FULL", l);
        b = new dza("PERSONAL", s);
        c = new dza("FLOATING", r);
        d = new dza("ACADEMIC", t);
        e = new dza("SITE", u);
        f = new dza("OS", o);
        g = new dza("EAP", n);
        h = new dza("KLEVAL", m);
        i = new dza("EVAL", m);
        j = new dza("INVALID", p);
    }

    // ...
}
</pre>
可以看出这是定义license类型的类
<pre class="lang:java decode:1 " >
package z;

public class aef extends hwn {
    // ...

    public static final aef a = new gdo("UserName");
    public static final aef b = new gdo("UserCompany");
    public static final aef c = new fsf("CustomerID");
    public static final aef d = new fir("ExpirationDate");
    public static final aef e = new aef("LicenseType", dza.class);
    public static final aef f = new gdo("AdditionalInfo");
    public static final aef g = new fsf("MinBuild");
    public static final aef h = new fsf("MaxBuild");
    public static final aef i = new fsf("MaxLeaseCount");
    public static final aef m = new fsf("R");
    public static final Date j = new Date(0L);
    public static final Date k = new Date(1L);

    // ...
}
</pre>
这个类定义了需要验证哪些内容，最后关键类的关键代码：
<pre class="lang:java decode:1 " >
package z;

public class huv implements cud {
    // ...

    public String a(aef aef1) {
        String s;

        if (aef1 == aef.d) {
            Date time = new Date(System.currentTimeMillis() + 24 * 60 * 60 * 1000);
            Calendar cal = Calendar.getInstance();
            cal.setTime(time);
            int year = cal.get(Calendar.YEAR);
            int month = cal.get(Calendar.MONTH) + 1;
            int day = cal.get(Calendar.DAY_OF_MONTH);

            s = "" + year;
            if (month < 10) {
                s += ("0" + month);
            }
            if (day < 10) {
                s += ("0" + day);
            }
        } else if (aef1 == aef.b) {
            s = "Nazca";
        } else if (aef1 == aef.f) {
            s = "to memorize my Macbook...";
        } else if (aef1 == aef.e) {
            return dza.a.h();
        } else if (aef1 == aef.a) {
            return "Cracked by Jay";
        } else if (aef1 == aef.i) {
            return "20";
        } else if (aef1 == aef.c) {
            return "1";
        } else {
            s = "";
        }

        return s;
    }

    // ...
}
</pre>
可以看出过期时间定为当前时间的后一天，这样就永远不会过期了。最后编译，打包，替换原先的jar包，就行了。

最后提一句，破解时选择切入点非常重要。比如这次，我选择的切入点是相当靠后的，仅仅在字符串被送入验证方法之前。如果切入点再往前的话会很麻烦，因为看了一下代码，deskzilla的license是一个经3DES加密的XML文件，XML还需要用MD5校验，如果切入点是生成XML文件，那我还得搞到3DES的密钥，以及保证MD5验证通过。所谓打蛇打七寸，选对了切入点，往往有事半功倍的效果。</pre>