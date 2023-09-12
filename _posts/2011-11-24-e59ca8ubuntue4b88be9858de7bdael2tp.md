---
id: 13085
title: 在Ubuntu下配置L2TP
date: '2011-11-24T01:47:32+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13085'
permalink: /2011/11/24/13085
views:
    - '10834'
shorturl:
    - 'http://goo.gl/rRRPn'
duoshuo_thread_id:
    - '6.3356049087498E+18'
dsq_thread_id:
    - '4271398230'
posturl_add_url:
    - 'yes'
---

由于CentOS下的yum远不如apt好用，于是花了两个晚上的时间把Linode上的系统从CentOS换成了Ubuntu。昨天重新搭了wordpress、git，今天把L2TP搞定了，参考了很多文章，主要有<a href="http://ubuntuforums.org/showthread.php?t=1645473" target="_blank">这篇</a>和<a href="http://apple4.us/2010/05/setting-up-l2tp-vpn-on-debian-ubuntu.html" target="_blank">这篇</a>，综合并整理了一下，贴在这里

Tips：在Linode上两个系统间迁移时，因为每次只能启动一个系统，原先以为得把文件从CentOS下到本地再传到Ubuntu，估计会很慢。后来想到能把原先的CentOS的磁盘直接在Ubuntu里mount，便能直接拷贝了
<h2>安装所需包</h2>
我用的Ubuntu是11.10，貌似下来xl2tpd是依赖于openswan和ppp的，于是直接安装xl2tpd
<pre class="lang:shell decode:1 " >
apt-get install xl2tpd
</pre>
<h2>配置</h2>
<h3>IPSec</h3>
编辑/etc/ipsec.conf，改成
<pre class="lang:shell decode:1 " >
version 2.0
config setup
    nat_traversal=yes
    virtual_private=%v4:10.0.0.0/8,%v4:192.168.0.0/16,%v4:172.16.0.0/12
    oe=off
    protostack=netkey

conn L2TP-PSK-NAT
    rightsubnet=vhost:%priv
    also=L2TP-PSK-noNAT

conn L2TP-PSK-noNAT
    authby=secret
    pfs=no
    auto=add
    keyingtries=3
    rekey=no
    ikelifetime=8h
    keylife=1h
    type=transport
    left=${your.server.ip.address}
    leftprotoport=17/1701
    right=%any
    rightprotoport=17/%any
</pre>
注意缩进，并替换${your.server.ip.address}为服务器公网IP地址

编辑/etc/ipsec.secrets，改成
<pre class="lang:shell decode:1 " >
${your.server.ip.address}    %any:    PSK    "${your.shared.secret}"
</pre>
替换IP地址和共享密钥

修改/etc/sysctl.conf，添加
<pre class="lang:shell decode:1 " >
net.ipv4.ip_forward = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0
</pre>
执行
<pre class="lang:shell decode:1 " >
sysctl -p
</pre>
令修改生效
<h3>XL2TPD</h3>
修改/etc/xl2tpd/xl2tpd.conf
<pre class="lang:shell decode:1 " >
[global]
ipsec saref = yes

[lns default]
ip range = 10.1.2.2-10.1.2.255
local ip = 10.1.2.1
refuse chap = yes
refuse pap = yes
require authentication = yes
ppp debug = yes
pppoptfile = /etc/ppp/options.xl2tpd
length bit = yes
</pre>
<h3>PPP</h3>
修改/etc/ppp/options.xl2tpd
<pre class="lang:shell decode:1 " >
require-mschap-v2
ms-dns 208.67.222.222
ms-dns 208.67.220.220
asyncmap 0
auth
crtscts
lock
hide-password
modem
debug
name l2tpd
proxyarp
lcp-echo-interval 30
lcp-echo-failure 4
</pre>
修改/etc/ppp/chap-secrets添加密码，格式：
<pre class="lang:shell decode:1 " >
&lt;用户名&gt;  &lt;名称，对应上面的name&gt;  &lt;密码&gt;
</pre>
添加iptables规则
<pre class="lang:shell decode:1 " >
iptables --table nat --append POSTROUTING --jump MASQUERADE
</pre>
并添加至/etc/rc.local
<h2>启动</h2>
<pre class="lang:shell decode:1 " >
service ipsec restart
service xl2tpd restart
</pre>
<h2>OK，连接成功，let's break the damn wall！</h2>