---
id: 13400
title: 'Enable HTTPS on Ubuntu'
date: '2012-03-31T13:59:57+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13400'
permalink: /2012/03/31/13400
posturl_add_url:
    - 'yes'
views:
    - '3264'
duoshuo_thread_id:
    - '6.3356049895153E+18'
dsq_thread_id:
    - '4288443409'
---

<b>Enable ssl site</b>
<pre class="lang:shell decode:1 " >
sudo a2ensite ssl
</pre>

<b>Enable ssl, rewrite mod</b>
<pre class="lang:shell decode:1 " >
sudo a2enmod rewrite
sudo a2enmod ssl
</pre>

<b>Add rewrite commands in /etc/apache2/sites-enabled/000-default, redirecting all connections on port 80 to https</b>
<pre class="lang:shell decode:1 " >
RewriteEngine   on
RewriteCond     %{SERVER_PORT} ^80$
RewriteRule     ^(.*)$ https://%{SERVER_NAME}$1 [L,R]
</pre>

<b>Restart Apache</b>
<pre class="lang:shell decode:1 " >
sudo service apache2 restart
</pre>
