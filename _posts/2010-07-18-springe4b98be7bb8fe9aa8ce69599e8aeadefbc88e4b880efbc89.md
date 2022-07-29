---
id: 2373
title: Spring之经验教训（一）
date: '2010-07-18T01:27:24+08:00'
author: Jay
layout: post
guid: 'http://jayxu.com/?p=2373'
permalink: /2010/07/18/2373
aktt_notify_twitter:
    - 'yes'
    - 'yes'
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
dsq_thread_id:
    - '4271398042'
views:
    - '3771'
shorturl:
    - 'http://goo.gl/bqNvl'
duoshuo_thread_id:
    - '6.335604609029E+18'
posturl_add_url:
    - 'yes'
---

<p>在现在的项目中我们使用了spring + hibernate + struts的架构，在享受aop, orm, ioc, di带来的种种便利的同时，我们亦遇到了很多莫名其妙或者说刻骨铭心的教训，今天先整理两点，日后继续补充</p>
<h4>经验一：时刻牢记，spring、hibernate对对象 进行了动态代理，尽量不要试图在动态代理后的对象上进行反射，尤其是field！</h4>
<p>不管是hibernate的orm还是spring的声明式事务管理，都对原来的pojo、dao进行了动态代理。虽然s、h&ldquo;号称&rdquo;动态代理做得天衣无缝且无色无味，但是，那只是在&ldquo;绝大多数情况下&rdquo;，如果想对动态代理后的对象进行反射，麻烦便来了，代码片段：</p>
<pre class="lang:java decode:1 " >
public static void setCreditInfoStatus(CreditInfo info, CreditType type, CreditValidateStatus status) {
    ...

    Field[] fields = CreditInfo.class.getDeclaredFields();

    for (Field f : fields) {
        if (f.isAnnotationPresent(Credit.class) &amp;&amp; f.getAnnotation(Credit.class).value() == type) {
            PropertyDescriptor pd = BeanUtils.getPropertyDescriptor(CreditInfo.class, f.getName());
            if (pd != null)  {
                ...
            }
            break;
        }
    }
}</pre>
<p>原先第7行写为 info.getClass()，乍一看与现有的代码功能上是一样的，但是别忘了让人又恨又爱的动态代理！上面代码返回的是真正的CreditInfo class，而左边的返回的是动态代理后的class，即意味着，第一个&ldquo;if&rdquo;永远返回的是false，除非动态代理后的对象的field上附带了原有的annotation</p>
<h4>经验二：spring的声明式事务管理确很强大，强大到可以支持多线程，但是，结合上一点，不要在线程中调用this中的事务方法</h4>
<p>声明式事务，即spring中使用aop织入或 @Transactional标记的方法注入事务容器，码农们可以完全不用操心何时begin，何时commit，何时 rollback，有没有嵌套，绝对傻瓜级的编程模型。但是，牢记，spring中的aop、annotation都是使用动态代理实现的，即，如果没有经过动态代理便也没有了事务管理，代码片段：</p>
<pre class="lang:java decode:1 " >public class AutomatedService{
    ...

    loanQueue.execute(new Runnable() {

        @Override
        public void run() {
            Thread thread =  Thread.currentThread();

            while (!thread.isInterrupted()) {
                try {
                    loanService.checkNSetLoanStatus();

                    Thread.sleep(loanStatusCheckIntervalMinutes * Consts.ONE_MINUTE);
                } catch (InterruptedException ex) {
                    thread.interrupt();
                }
            }
        }
    });

    ...
}</pre>
<p>原先的checkNSetLoanStatus方法是定义在AutomatedService中的，且标记了@Transactional。 但是，令人发指的是，checkNSetLoanStatus中的事务没有被提交。在痛定思痛仔细回想了spring的声明式事务的本质后，豁然发现当调用this.checkNSetLoanStatus()时，并没有被织入事务管理。spring还没有霸道到或者说聪明到对this进行动态代理，于是将该方法移至其它service并注入，问题解决</p>
