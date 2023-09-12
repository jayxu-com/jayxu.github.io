---
id: 16193
title: 'Mac OS X升个级，Java（&#038;其它各种）社区鸡飞狗跳……'
date: '2017-09-22T12:08:27+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=16193'
permalink: /2017/09/22/16193
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '3161'
image: /log/wp-content/uploads/2017/09/fake-kernel-panic.jpg
---

<!-- wp:image {"id":16460} -->
<figure class="wp-block-image"><img src="https://i1.wp.com/www.jayxu.com/log/wp-content/uploads/2017/09/fake-kernel-panic.jpg?fit=619%2C341&amp;ssl=1" alt="" class="wp-image-16460" /></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>自从乔大爷走后，苹果整体给我的感觉是，除了越来越不会做产品，软件质量管理也已经是小公司的水准了……而这一感觉，在最新的Mac OS X 10.13 High Sierra（Tim Cook给OS起名字的能力从Mavericks开始就已经无力吐槽了……）以及iOS 11中集中爆发</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>作为一个从Tiger开始就重度使用Mac OS，且非常不安分有升级强迫症的资深用户，根据十几年的经验，苹果对于系统版本的发布节奏，在Cook之前一般1～2年一个新版本，期间会有4个左右DP（devepoer preview），1～3个PP（public preview），然后正式发布GM（golden master）。PP一般已经是很稳定的版本，跟GM在稳定性上几乎没有太大区别，所以一般尝鲜新版本会从PP开始。GM发布后，除非遇到安全漏洞或重大更新，否则在下一个大版本发布前顶多只会有2、3个小版本发布</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>而这一次，我如果没记错的话，High Sierra发布前出了6个DP，6个PP（貌似苹果现在的发布策略改了，在每个DP后一周都会有一个对应的PP发布）不同的DP间各种bug满天飞，还随机地飞，比如一个bug在DP 1中就有了，在DP 2中被修复，结果DP 5又出现了……到正式的GM发布后，依然一堆bug……GM后几乎2～3周一个DP/PP，2个月左右一个小版本GM。这种更新频率发生在苹果身上，在之前是无法想象的。我觉得只能反映出目前苹果对于软件产品管理的无能以及工程质量保障的失控。乔大爷要在天有灵，绝对能被气死，而且还得是好几回……</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>下面就说一个例子，Java相关。安装完10.13某一个DP后，我的Eclipse打开是这样的：</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":16278} -->
<figure class="wp-block-image"><a href="http://www.jayxu.com/log/wp-content/uploads/2018/03/menus.png"><img src="https://i0.wp.com/www.jayxu.com/log/wp-content/uploads/2018/03/menus.png?fit=1722%2C1700&amp;ssl=1" alt="" class="wp-image-16278"/></a></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>即所有的菜单项都无法点击，我开始以为是Eclipse对于Mac OS新版兼容性有问题，但在试了Netbeans、Xmind、DbVisualizer等其它Mac下的Java应用后，发现结果是一样的……于是同时给Mac OS、Eclipse开了bug：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul>
    <li>Eclipse上经过搜索已经有人开了bug：<a target="_blank" href="https://bugs.eclipse.org/bugs/show_bug.cgi?id=520176" rel="noopener noreferrer">[10.13] Menu Bar Disabled From Use Completely</a>，于是comment + vote。如果花点时间看下整个thread，会发现这个bug在不同beta间反反复复出现、消失了好几次，真不知道苹果的QA是干什么吃的</li>
    <li>苹果上我在两个版本上连开了两次（33507576和34508258）。由于苹果现在的bug report权限私有了，截下屏</li>
</ul>
<!-- /wp:list -->

<!-- wp:gallery {"columns":1,"linkTo":"media"} -->
<ul class="wp-block-gallery alignnone columns-1 is-cropped">
    <li class="blocks-gallery-item">
        <figure><a href="http://www.jayxu.com/log/wp-content/uploads/2017/09/33507576.png"><img src="http://www.jayxu.com/log/wp-content/uploads/2017/09/33507576.png" alt="" data-id="16332" data-link="http://www.jayxu.com/?attachment_id=16332"/></a></figure>
    </li>
    <li class="blocks-gallery-item">
        <figure><a href="http://www.jayxu.com/log/wp-content/uploads/2017/09/34508258.png"><img src="http://www.jayxu.com/log/wp-content/uploads/2017/09/34508258.png" alt="" data-id="16333" data-link="http://www.jayxu.com/?attachment_id=16333"/></a></figure>
    </li>
</ul>
<!-- /wp:gallery -->

<!-- wp:paragraph -->
<p>High Sierra GM发布之后，更奇葩的事情发生了，<a href="https://spring.io/blog/2017/09/21/how-to-get-sts-eclipse-running-on-macos-high-sierra-10-13">Spring</a>、<a href="https://www.eclipse.org/org/press-release/20170925criticalbug.php">Eclipse</a>竟然分别发布how-to，公告天下“怎么在High Sierra下正确地（通过hack一些文件才能）使用”相关应用。这种事情如果发生在m$身上我觉得没什么奇怪的，但是这次是苹果……我觉得开源社区怎么做，1. 甩锅，菜单看不见是苹果的锅，跟我们没关系；2. 狠狠地抽苹果的脸，竟然能把操作系统发布成这操性</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>2018-3-14补</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Java菜单门没过多久，N卡驱动门又开始了。如果你是N卡的苹果设备，我不知道你用High Sierra是什么感觉，反正我的感觉是相当酸爽……我的版本是刚发布的10.13.4 beta 5（17E182a），N卡。在窗口切换、滚屏、切换输入法等操作时系统会各种卡顿，甚至在iTunes听歌跳下一首时都会卡顿。遇到最丧心病狂的，是打开terminal，前面用Chrome窗口完全挡上，在Chrome里滚动页面内容，那种卡顿是当年在Win 95中都不曾体验过的……</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>有兴趣的同学网上可以去搜下“high sierra gpu glitch”，你会发现铺天盖地的讨论，比如Chrome中开的一个bug：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a target="_blank" href="https://bugs.chromium.org/p/chromium/issues/detail?id=773705#c168" rel="noopener noreferrer">Rendering glitches in High Sierra (macOS 10.13)</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>现在10.13.4已经beta 5了，照Cook的更新节奏，应该在下周或月底就会正式发布。但在发布时由N卡GPU导致的系统卡顿能否彻底解决，实话实说，我没抱希望……</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Mac OS，你现在还敢嘲笑Windows么？！</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":16407} -->
<figure class="wp-block-image"><img src="https://i0.wp.com/www.jayxu.com/log/wp-content/uploads/2018/03/zv6jf.png?resize=320%2C320&amp;ssl=1" alt="" class="wp-image-16407" /></figure>
<!-- /wp:image -->