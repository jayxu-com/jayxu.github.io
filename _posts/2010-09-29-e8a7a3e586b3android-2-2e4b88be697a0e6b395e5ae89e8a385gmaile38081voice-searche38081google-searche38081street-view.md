---
id: 2433
title: '解决android 2.2下无法更新gmail、voice search、google search、street view'
date: '2010-09-29T00:48:05+08:00'
author: Jay
layout: post
guid: 'http://jayxu.com/?p=2433'
permalink: /2010/09/29/2433
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
dsq_thread_id:
    - '4271399343'
views:
    - '7678'
shorturl:
    - 'http://goo.gl/tLMPx'
duoshuo_thread_id:
    - '6.3356046564833E+18'
---

最近android market接连推送了gmail（2.3）、voice search（2.0.1）、google search（1.1.1.53565）、street view（1.6.0.6）的更新，但是很不幸，通过market无法正常更新，每次总是烦人的“安装失败”。在经过了N久的尝试后，今天晚上终于更新成功！这里分享一下

首先去market下载安装TitaniumBackup，打开，获取root权限，进入“备份/还原”，找到要更新的程序，然后卸载，如下图：

<a href="http://jayxu.com/log/wp-content/uploads/2010/09/screenshot_2.png"><img class="alignnone size-full wp-image-2434" title="screenshot_2" src="http://jayxu.com/log/wp-content/uploads/2010/09/screenshot_2.png" alt="" width="320" height="480" /></a>

全部卸载后重启手机（这步很重要，之前我就是卸载后没重启导致再次安装失败），进入market，即可正常安装上面的软件了

我的ROM：Cyanogen Mod，cm_hero-09252010-011011