---
id: 17270
title: 'iPhone破解：1.0.2 -> 1.1.3'
date: '2021-01-24T11:59:52+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/2021/01/24/17270'
permalink: '/?p=17270'
---

<!-- wp:paragraph -->
<p>今天在公司玩iPhone，1.0.2的版本，心血来潮，决定升级。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>上网搜了N久，有不少升级的方法， 尝试了一种先升到1.1.1的，结果不能识别SIM卡。于是抱着iBrick的决心，直接升到1.1.3，结果成了，方法如下：</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li>下载1.1.3的更新文件，网上一搜一堆，以ipsw 为后缀，162兆</li><li>下载安装最新的iTunes，直接上苹果的官网下</li><li>连上iPhone，双击1中下载的ipsw，这时应打开iTunes进行更新，更新完后会重启，但处于锁定状态</li><li>更新完后，上网搜一个叫ZiPhone的东西，有带GUI的版本，当前好像是3.1</li><li>打开ZiPhone（我用的GUI版本，会安装一下），连上iPhone，单击ZiPhone里的“Free My iPhone”，这时iPhone会重启，不行的话重启iPhone，再试一次。成功的话会看到iPhone在刷屏，2分钟左右以后iPhone自动重启，破解完成！</li><li>在iphone桌面按installer图标进入install按次序安装Community Sources、BSD system 2.0 Termfix、BSD system 2.1和open SSH</li><li>在 iphone里点击setting -&gt; general -&gt; network -&gt; wifi里看到你的iPhone的IP地址</li><li>下载安装Winscp，打开Winscp，在Winscp里输入<br>ip：192.168.1.100<br>用户名：root<br>密码：alpine<br>按LOGIN，一次连接大约需要30-45秒。别急，连不上的话多试几次。</li><li>下载iphone 1.1.3汉化包，然后解压。用Winscp 将解压出的2个文件夹Applications和System传到 iphone的根目录下，覆盖原文件</li><li>在iPhone 里点击setting -&gt; general -&gt; international -&gt; language -&gt; 简体中文</li><li>在iPhone里点击 设置 -&gt; 通用 -&gt; 自动锁定 -&gt; 永不</li><li>在iPhone里点击打开installer，选择source -&gt; edit -&gt; add，填入http://app.weiphone.com/installer</li><li>在installer里找到weiphone -&gt; WeFit安装</li><li>完成后重启iPhone，大功告成！</li></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>刷屏中……</p>
<!-- /wp:paragraph -->

<!-- wp:image {"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="http://www.jayxu.com/log/wp-content/uploads/2008/03/p1010675.JPG"><img src="http://www.jayxu.com/log/wp-content/uploads/2008/03/p1010675.JPG" alt=""/></a></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>刷完后，中文版，可输入中文</p>
<!-- /wp:paragraph -->

<!-- wp:image {"linkDestination":"media"} -->
<figure class="wp-block-image"><a href="http://www.jayxu.com/log/wp-content/uploads/2008/03/p1010676.JPG"><img src="http://www.jayxu.com/log/wp-content/uploads/2008/03/p1010676.JPG" alt=""/></a></figure>
<!-- /wp:image -->