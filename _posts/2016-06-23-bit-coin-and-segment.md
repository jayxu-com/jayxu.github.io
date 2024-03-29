---
id: 14706
title: '揭秘比特币和区块链（一）：什么是区块链？ [zz]'
date: '2016-06-23T16:37:12+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=14706'
permalink: /2016/06/23/14706
posturl_add_url:
    - 'yes'
views:
    - '2986'
dsq_thread_id:
    - '4932360756'
duoshuo_thread_id:
    - '6.3356052385395E+18'
image: /log/wp-content/uploads/2016/06/1394520101341.jpg
---

原文转自：<a href="http://www.infoq.com/cn/articles/bitcoin-and-block-chain-part01" target="_blank">InfoQ</a>
<h2>比特币的背景知识</h2>
随着信息技术的发展，人们的生活逐渐网络化，数字化。人类社会因此发生着深刻的变化。对数字货币的探索，就是在这样的背景下应运而生的。其实相关的研究在上世纪八九十年代，就开始了。

在数字货币的探索实践中，比特币是目前表现最好的一个。说到比特币的缘起，就不得不谈到一个略显神秘的团体：密码朋克（CypherPunk）。这个团体是密码天才们的松散联盟。在比特币的创新中，大量借鉴了密码朋克成员的贡献。

密码朋克本身就是数字货币最早的传播者，在其电子邮件组中，常见关于数字货币的讨论，并有一些想法付诸实践。在比特币之前，有很多失败的尝试。在这里我们简要列举一些之前探路者。
<ul>
 	<li><b>亚当·贝克</b>（Adam Back）是一位英国的密码学家，1997年，他发明了哈希现金（hashcash）[i]，其中用到了工作量证明机制（proof of work）。这个机制的原型是用于解决互联网垃圾信息问题的[ii]。工作量证明机制后来成为比特币的核心要素之一。</li>
 	<li><b>哈伯和斯托尼塔</b>（Haber and Stornetta）在1997年提出了一个用时间戳的方法保证数字文件安全的协议[iii]，这个协议成为比特币区块链协议的原型。</li>
 	<li><b>戴伟</b>（W Dai）是一位兴趣广泛的密码学专家，他在1998年发明了B-money[iv]，B-money强调点对点的交易和不可更改的交易记录。不过在B-money中，每台计算机各自单独书写交易记录，这很容易造成系统被账本的不一致。戴伟为此设计了复杂的奖惩机制以防止作弊，但是并没有能从根本上解决问题。中本聪发明比特币的时候，借鉴了很多戴伟的设计，并和戴伟有很多邮件交流。</li>
 	<li><b>哈尔·芬尼</b>（Hal Finney））是PGP公司的一位顶级开发人员，也是密码朋克运动早期和重要的成员。2004年，芬尼推出了自己版本的电子货币，在其中采用了可重复使用的工作量证明机制（RPOW）。哈尔·芬尼是第一笔比特币转账的接受者，在比特币发展的早期与中本聪有大量互动与交流。由于身患绝症，哈尔·芬尼已于2014年去世。</li>
</ul>
&nbsp;
<h2>比特币的诞生</h2>
2008年9月，以雷曼兄弟的倒闭为开端，金融危机在美国爆发并向全世界蔓延。为应对危机，各国政府采取量化宽松等措施，救助由于自身过失、陷入危机的大型金融机构。这些措施带来了广泛的质疑，并一度引发了“占领华尔街”运动。

2008年10月31日纽约时间下午2点10分，在一个普通的密码学邮件列表中，几百个成员均收到了自称是中本聪的人的电子邮件[v]，“我一直在研究一个新的电子现金系统，这完全是点对点的，无需任何可信的第三方”，然后他将他们引向一个九页的白皮书，其中描述了一个新的货币体系。同年11月16日，中本聪放出了比特币代码的先行版本[vi]。

2009年1月3日，中本聪在位于芬兰赫尔辛基的一个小型服务器上挖出了比特币的第一个区块——创世区块（Genesis Block），并获得了首矿”奖励——50个比特币。在创世区块中，中本聪写下这样一句话：
<blockquote>The Times 03/Jan/2009 Chancellor on brink of second bailout for banks

财政大臣站在第二次救助银行的边缘</blockquote>
&nbsp;

这句话是当天泰晤士报头版的标题。中本聪将它写进创世区块，不但清晰地展示着比特币的诞生时间，还表达着对旧体系的嘲讽。

如今，比特币已经成为数字货币领域的翘楚，拥有数十亿美元的市值，但中本聪却于2010年选择隐退。中本聪是谁，对每一个开始了解比特币的人，都是感兴趣的话题。从《纽约客》到《新闻周刊》，媒体们找到了数个自称是中本聪，或者被认为是中本聪的人。但无一例外，这些发现都因为可信度不足，遭到了读者甚至是中本聪本人的否定。中本聪是谁？也许我们永远不得而知。

&nbsp;
<h2>比特币与区块链</h2>
比特币已经在争议中走过了7年多的历程。在历史上，很少有这样一种东西，人们对待它的态度如此泾渭分明，支持者认为它将改变世界，反对者认为它毫无价值。望文生义，很容易得出后一个结论。“币”这个词虽然准确的描述了其金融属性，但由于过于形象，使得大多数人对于它如何能与完全虚拟的“比特”关联起来而大惑不解。

其实，在比特币的系统中，最重要的并不是“币”的概念，而是一个没有中心存储机构的“账本”的概念。“币”只是在这个账本上使用的记账单位。可以这么说，比特币本质就是一个基于互联网的去中心化账本，而区块链就是这个账本的名字。这里我们可以做一个形象的类比，假如区块链是一个实物账本，一个区块就相当于账本中的一页，区块中承载的信息，就是这一页上记载的交易内容。

<i><u><strong>区块链是比特币的核心与基础架构，是一个去中心化的账本系统。</strong></u></i>

既然区块链是个账本，这个账本和我们传统的账本有什么不同？我们知道，账本上的内容必须是唯一的，这导致记账天然是中心化的行为。在通讯手段不发达的时代如此，在现今的信息时代也是如此。然而，中心化的记账却有一些显而易见的弱点：一旦这个中心出现问题，如被篡改、被损坏，整个系统就会面临危机乃至崩溃。

那么问题来了——<b>我们能不能构建一个去中心化的不依赖任何第三方的但却可信的记账系统呢？</b>去中心记账可以克服中心化账本的弱点，但是想实现这样的账本系统绝非易事。

在数字时代，负责记账的自然是计算机。这里，我们把记账系统中接入的每一台计算机称为“节点”。去中心化就是没有中心，也就是说参与到这个系统中的每个节点都是中心。从设计账本系统的角度，就是需要每个节点都保存一份完整的账本。然而，由于一致性的要求，每个节点却不能同时记账。因为节点所处的环境不同，接收到的信息自然不同，如果同时记账的话，必然会导致账本的不一致，造成混乱。

既然节点不能同时记账，那我们就不得不选择哪个节点拥有记账的权力。但是，如果指定某些特殊节点拥有记账的权力，势必又会与我们去中心化的初衷相违背。

这似乎成了不可能解决的问题。

&nbsp;
<h2>竞争记账和激励机制</h2>
中本聪设计的比特币区块链通过竞争记账的方式解决了去中心化的记账系统的一致性问题。

前面提到，节点可以理解为接入系统中的计算机，而所谓的竞争记账，就是以每个节点的计算能力即“算力”来竞争记账权的一种机制。在比特币系统中，大约每十分钟进行一轮算力竞赛（算力大小会决定赢得一轮竞争的概率，算力高的节点赢得算力竞争的概率更大），竞赛的胜利者，就获得一次记账的权力，这样，一定时间内，只有竞争的胜利者才能记账并向其他节点同步新增账本信息。

那么，在一个去中心化的系统中，谁有权判定竞争的结果呢？比特币系统是通过一个称为“工作量证明”（proof of work, POW）的机制完成的。举个简单的例子，比如说要生产一些玩具，早上起来我给你一些零件，晚上回来，看到需要的玩具摆在桌上，虽然我没有从早到晚盯着你做玩具的过程，我也能确定你确实做了这么多工作。这就是工作量证明简单的理解——通过一个（人人都可以验证的）特定的结果就能确认（竞争的）参与者完成了相应的工作量。（关于POW的机制与实现细节，会在接下来的文章中详述）

算力竞争是要付出成本的，没有激励，节点就没有进行竞争的动力。在中本聪的设计里，每轮竞争胜出并完成记账的节点，将可以获得系统给予的一定数量的比特币奖励[vii]。而这个奖励的过程，同时也是比特币的发行过程。这种设计相当巧妙 —— 它将竞争的激励机制与货币的发行完美结合到一起，在引入竞争的同时，解决了去中心化货币系统中发行的难题。

在这个系统中，每一个节点只需要根据自身利益行事。出于“自私”的目的进行的竞争，最终造就了保护系统安全的庞大算力基础。在这样精巧的安排下，比特币获得了越来越多的信任，和越来越高的价值，进而又吸引了更多的资源投入其中，成为一个正向循环的经济系统。

正因为比特币通过区块链的机制造就了这样一个正向循环的经济系统，才会在没有强大的中心化机构推动的情况下，自然的生长出来并发展壮大。

读到这里，显然我们会发现，虽然区块链脱胎于比特币，但区块链无论作为一个系统还是作为一项技术，它的应用领域及发展潜力，将远不止货币。之后的文章，我们会通过更加深入的分析与讲解，带您深入到区块链的原理与实现细节。

&nbsp;
<h2>参考文档与备注</h2>
[i] <a href="http://www.hashcash.org/papers/announce.txt">http://www.hashcash.org/papers/announce.txt</a>

[ii] <a href="https://en.wikipedia.org/wiki/Cynthia_Dwork">Dwork, Cynthia</a>; <a href="https://en.wikipedia.org/wiki/Moni_Naor">Naor, Moni</a> (1993). <a href="http://www.wisdom.weizmann.ac.il/~naor/PAPERS/pvp.ps">"Pricing via Processing, Or, Combatting Junk Mail, Advances in Cryptology"</a>. <i>CRYPTO’92: Lecture Notes in Computer Science No. 740</i>(Springer): 139–147.

[iii] S. Haber, W.S. Stornetta, “Secure names for bit-strings,” In Proceedings of the 4th ACM Conference on Computer and Communications Security, pages 28-35, April 1997. on Computer and Communications Security, pages 28-35, April 1997.

[iv] W Dai,a scheme for a group of untraceable digital pseudonyms to pay each other with money and to enforce contracts amongst themselves without outside help “B-money”,<a href="http://www.weidai.com/bmoney.txt">http://www.weidai.com/bmoney.txt</a>, 1998<a href="http://www.8btc.com/wiki/bitcoin-a-peer-to-peer-electronic-cash-system#refmark-1">↵</a>

[v] <a href="http://www.mail-archive.com/cryptography@metzdowd.com/msg09959.html">http:<span class="__cf_email__" data-cfemail="fed1d1898989d0939f9792d39f8c9d9697889bd09d9193d19d8c878e8a91998c9f8e9687be939b8a849a91899ad09d9193">[email protected]</span><script type="text/javascript" data-cfhash="f9e31">// <![CDATA[
// < ![CDATA[
// < ![CDATA[ !function(t,e,r,n,c,a,p){try{t=document.currentScript||function(){for(t=document.getElementsByTagName('script'),e=t.length;e--;)if(t[e].getAttribute('data-cfhash'))return t[e]}();if(t&&(c=t.previousSibling)){p=t.parentNode;if(a=c.getAttribute('data-cfemail')){for(e='',r='0x'+a.substr(0,2)|0,n=2;a.length-n;n+=2)e+='%'+('0'+('0x'+a.substr(n,2)^r).toString(16)).slice(-2);p.replaceChild(document.createTextNode(decodeURIComponent(e)),c)}p.removeChild(t)}}catch(u){}}()
// ]]></script>/msg09959.html</a>

[vi] <a href="http://www.mail-archive.com/cryptography@metzdowd.com/msg10142.html">http:<span class="__cf_email__" data-cfemail="426d6d3535356c2f232b2e6f2330212a2b34276c212d2f6d21303b32362d253023322a3b022f273638262d35266c212d2f">[email protected]</span><script type="text/javascript" data-cfhash="f9e31">// <![CDATA[
// < ![CDATA[
// < ![CDATA[ !function(t,e,r,n,c,a,p){try{t=document.currentScript||function(){for(t=document.getElementsByTagName('script'),e=t.length;e--;)if(t[e].getAttribute('data-cfhash'))return t[e]}();if(t&&(c=t.previousSibling)){p=t.parentNode;if(a=c.getAttribute('data-cfemail')){for(e='',r='0x'+a.substr(0,2)|0,n=2;a.length-n;n+=2)e+='%'+('0'+('0x'+a.substr(n,2)^r).toString(16)).slice(-2);p.replaceChild(document.createTextNode(decodeURIComponent(e)),c)}p.removeChild(t)}}catch(u){}}()
// ]]></script>/msg10142.html</a>

[vii] 记账奖励包括一个数量的比特币和该区块包含的所有交易的手续费。系统发放的记账奖励每四年进行一次减半。最开始为50币/区块，目前为25币/区块，以此类推，直到系统中的总币数达到2100万的上限。