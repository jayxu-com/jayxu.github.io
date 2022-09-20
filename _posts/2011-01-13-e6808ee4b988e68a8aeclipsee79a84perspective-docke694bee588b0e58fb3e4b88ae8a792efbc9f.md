---
id: 10426
title: '怎么把Eclipse的perspective dock放到右上角？'
date: '2011-01-13T18:29:38+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=10426'
permalink: /2011/01/13/10426
aktt_tweeted:
    - '1'
    - '1'
aktt_notify_twitter:
    - 'yes'
    - 'yes'
views:
    - '5522'
shorturl:
    - 'http://goo.gl/pB6lk'
duoshuo_thread_id:
    - '6.3356047143689E+18'
dsq_thread_id:
    - '4467468912'
posturl_add_url:
    - 'yes'
---

Eclipse很强大，osgi很灵活，PDE扩展性很强，但是，PDE实在太huge了，加上各种各样的plugin提供的extension point，以及仅仅org.eclipse.ui提供的workbench，workbenchwindow，menumanager，coolbarmanager，toolbarmanager……文档、javadoc就够你受的。今天在修一个issue，很简单，我们实现了一个standalone的基于PDE的界面，可不知道为什么，perspective dock默认出现在了左边（图一），而用户希望出现在常见的右边（图二）

[caption id="attachment_10430" align="alignnone" width="480" caption="图一"]<a href="http://www.jayxu.com/log/wp-content/uploads/2011/01/left1.png"><img class="size-medium wp-image-10430" title="left" src="http://www.jayxu.com/log/wp-content/uploads/2011/01/left1.png" alt="" width="480" height="337" /></a>[/caption]

[caption id="attachment_10431" align="alignnone" width="480" caption="图二"]<a href="http://www.jayxu.com/log/wp-content/uploads/2011/01/right1.png"><img class="size-medium wp-image-10431" title="right" src="http://www.jayxu.com/log/wp-content/uploads/2011/01/right1.png" alt="" width="480" height="337" /></a>[/caption]

看上去很简单，但是搞了半天没有搞定，上网google，找到了<a href="http://www.eclipse.org/forums/index.php?t=thread&amp;frm_id=106" target="_blank">这篇</a>和<a href="http://www.vogella.de/articles/EclipseCommands/article.html" target="_blank">这篇</a>，结论很简单，要想把dock放到右边，得调用IWorkbenchWindowConfigurer.setShowCoolBar(true);；要拿到IWorkbenchWindowConfigurer的对象，得继承IApplication，然后继承WorkbenchAdvisor，然后继承WorkbenchWindowAdvisor，最后覆盖WorkbenchWindowAdvisor.preWindowOpen()……反正就是得搞出三个类，覆盖三个方法……虽然看着麻烦点，但是能搞定的。然而，对于非standalone的PDE应用，你是不可能继承IApplication的，因为程序入口由Eclipse接管，而不是IApplication……于是上面这些research都是白做……

于是开始看源代码，然后静态分析上面各个方法的调用关系，最后找到了这么一个方法：WorkbenchWindow.setPerspectiveBarLocation(IWorkbenchPreferenceConstants.TOP_RIGHT);，于是把着个方法放到Activator的子类里，比如这样：
<pre class="lang:java decode:1 " >
public class CompActivator extends AbstractUIPlugin {

    @Override
    public void start(BundleContext context) throws Exception {
        super.start(context);

        ...

        // put perspective dock to top-right
        ((WorkbenchWindow) this.getWorkbench().getActiveWorkbenchWindow())
            .setPerspectiveBarLocation(IWorkbenchPreferenceConstants.TOP_RIGHT);
    }
}
</pre>
p.s. 可气的是，在看源代码的过程中，IWorkbenchWindowConfigurer.setShowCoolBar(boolean)的实现里有这么一句注释（368行）：“@issue need to be able to reconfigure after window's controls created”，MF！