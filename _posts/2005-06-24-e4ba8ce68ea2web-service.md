---
id: 213
title: '二探Web service'
date: '2005-06-24T17:43:00+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/log/?p=213'
permalink: /2005/06/24/213
aktt_notify_twitter:
    - 'yes'
    - 'yes'
views:
    - '3595'
shorturl:
    - 'http://goo.gl/1HvRd'
duoshuo_thread_id:
    - '6.3356039373783E+18'
dsq_thread_id:
    - '4361858504'
---

复习了一天体系结构，打开JB玩玩Web service消遣消遣。发现WSDL的描述文件支持用户自定义类，但不支持JDK中的类库，应该是因为C#中没有相应的类与之对应，好像比较麻烦。如果要真正做到Java与.net无障碍协作的话得把JDK中所有的类在.net端映射一下。但如果是小范围应用的话可以考虑适配器模式（Adapter） :idea: