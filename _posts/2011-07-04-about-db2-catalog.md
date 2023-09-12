---
id: 10658
title: 'About DB2 Catalog'
date: '2011-07-04T13:59:52+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=10658'
permalink: /2011/07/04/10658
aktt_notify_twitter:
    - 'yes'
views:
    - '3498'
aktt_tweeted:
    - '1'
dsq_thread_id:
    - '4288469597'
shorturl:
    - 'http://goo.gl/fg4sr'
duoshuo_thread_id:
    - '6.3356048239283E+18'
---

<h3>Catalog node/database</h3>
node:
<pre lang="sql">catalog tcpip node &lt;node_name&gt; remote &lt;hostname&gt; server &lt;port_number&gt;</pre>
databse:
<pre lang="sql">catalog database &lt;database_name&gt; as &lt;database_alias&gt; at node &lt;node_name&gt;</pre>
<h3></h3>
<h3>Uncatalog node/database</h3>
node:
<pre lang="sql">uncatalog node &lt;node_name&gt;</pre>
databse:
<pre lang="sql">uncatalog database &lt;database_alias&gt;</pre>