---
id: 14676
title: 'Tips：解决Mac OS X系统语言与登录界面语言不一致的问题'
date: '2016-03-21T09:38:18+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=14676'
permalink: /2016/03/21/14676
posturl_add_url:
    - 'yes'
views:
    - '5786'
dsq_thread_id:
    - '4679493735'
hefo_before:
    - '0'
hefo_after:
    - '0'
duoshuo_thread_id:
    - '6.3356052384933E+18'
image: 'https://d1k8eqsfs47rrv.cloudfront.net/log/wp-content/uploads/2016/03/终端_—_-zsh_—_zsh_—_⌘1.png'
---

最近El Capitan下一个问题一直很困扰强迫症的我：即使将操作系统语言设成简体中文，登录界面依然是英文……上网搜了一下之后，<a href="http://www.tip4mac.com/2011/10/fixing-the-issue-login-screen-lang-differ-from-system-lang/" target="_blank">Tip4Mac</a>上的一篇博客解决了我的问题：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/03/语言与地区.png" rel="attachment wp-att-14677"><img class="alignnone size-medium wp-image-14677" src="http://www.jayxu.com/log/wp-content/uploads/2016/03/语言与地区-600x408.png" alt="语言与地区" width="600" height="408" /></a>

进入终端，输入命令
<blockquote>
<pre class="inline:true decode:1">sudo languagesetup
</pre>
</blockquote>
&nbsp;

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/03/终端_—_-zsh_—_zsh_—_⌘1.png" rel="attachment wp-att-14678"><img class="alignnone size-medium wp-image-14678" src="http://www.jayxu.com/log/wp-content/uploads/2016/03/终端_—_-zsh_—_zsh_—_⌘1-600x621.png" alt="终端_—_-zsh_—_zsh_—_⌘1" width="600" height="621" /></a>

然后在菜单中选择“ 4) 以简体中文作为主要语言”即可