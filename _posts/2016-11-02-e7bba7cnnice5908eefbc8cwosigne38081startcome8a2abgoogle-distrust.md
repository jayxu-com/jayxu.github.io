---
id: 15938
title: '继CNNIC后，WoSign、StartCom被Google distrust'
date: '2016-11-02T19:12:28+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15938'
permalink: /2016/11/02/15938
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '5075'
dsq_thread_id:
    - '5272440608'
image: /log/wp-content/uploads/2016/11/201512095561449652247953.jpg
---

<a href="https://security.googleblog.com/2015/03/maintaining-digital-certificate-security.html" target="_blank">去年</a>是CNNIC（国字头的“中国互联网络信息中心”，12306网站证书的签发单位）

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG121.jpeg"><img class="alignnone size-medium wp-image-15939" src="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG121-640x312.jpeg" alt="" width="640" height="312" /></a>

<a href="https://security.googleblog.com/2016/10/distrusting-wosign-and-startcom.html?m=1" target="_blank">这次</a>是WoSign

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG120.jpeg"><img class="alignnone size-medium wp-image-15942" src="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG120-640x417.jpeg" alt="" width="640" height="417" /></a>

这么多年Google仅有的几个distrust CA根证书的案例两个给了中国的CA。哦不对，是两个半，今年9月<a href="http://weibo.com/ttarticle/p/show?id=2309404021487999802068#_0" target="_blank">WoSign入股了StartCom</a>……

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG122.jpeg"><img class="alignnone size-medium wp-image-15941" src="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG122-640x358.jpeg" alt="" width="640" height="358" /></a>

失信这件事目前在我朝可能还不是一件特别大、特别严肃的事，但在国际范围内尤其是数字证书这个特定的领域，一次失信被坐实带来的后果是没有后悔药的，这也是为什么一直到现在使用Chrome、Safari、FF等浏览器打开12306订票网站仍是个红叉甚至无法打开了

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG123.jpeg"><img class="alignnone size-medium wp-image-15940" src="http://www.jayxu.com/log/wp-content/uploads/2016/11/WechatIMG123-640x379.jpeg" alt="" width="640" height="379" /></a>

当然，12306用政府公信力做背书让不明真相的群众安装并信任证书绕过浏览器安全机制的做法是另一个话题了。失信一次就被distrust（而且Google还在呼吁FF、Safari等浏览器，以及微软、苹果、Linux社区等操作系统开发商一致行动），这不是小题大做，有兴趣的同学可以自行百度去年CNNIC为什么被distrust，再查下CA根证书到底意味着什么、相应的责任义务是什么，以及什么叫“中间人攻击”，就能明白这两次事件中，CNNIC、WoSign、Google到底是谁“别有用心”了