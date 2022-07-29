---
id: 13076
title: 'Ubuntu下启用Apache rewrite mod'
date: '2011-11-23T01:16:39+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13076'
permalink: /2011/11/23/13076
views:
    - '2876'
shorturl:
    - 'http://goo.gl/Ixu5h'
duoshuo_thread_id:
    - '6.3356049087078E+18'
dsq_thread_id:
    - '4288421497'
---

<pre lang="bash">sudo a2enmod rewrite
sudo vim /etc/apache2/sites-available/default
# 把所有 AllowOverride None 改成 AllowOverride All
sudo service apache2 restart</pre>
