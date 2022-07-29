---
id: 13377
title: 'Import PGP keys to resolve NO_PUBKEY issue'
date: '2012-03-28T02:23:43+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13377'
permalink: /2012/03/28/13377
posturl_add_url:
    - 'yes'
views:
    - '2990'
duoshuo_thread_id:
    - '6.3356049620426E+18'
dsq_thread_id:
    - '4438955278'
---

<pre class="lang:shell decode:1 " >
aptitude update 2>&1 > /dev/null | grep NO_PUBKEY | sed 's/^.*NO_PUBKEY //g' | xargs -L 1 gpg --keyserver keyserver.ubuntu.com --recv-keys; gpg --armor --export | apt-key add -
</pre>