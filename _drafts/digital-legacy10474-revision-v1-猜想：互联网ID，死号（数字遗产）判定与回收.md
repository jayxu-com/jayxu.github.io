---
id: 18484
title: 猜想：互联网ID，“死号”（数字遗产）判定与回收
date: '2023-05-24T13:31:50+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/?p=18484'
permalink: '/?p=18484'
---

<!-- wp:paragraph -->
<p><span style="color: #ff0000;"><span style="text-decoration: underline;">注：本文所有内容均为100%原汁原创，允许转载，但转载前请发邮件至mustangxu@gmail.com或评论告之，并在转载时附加出处信息，多谢配合！</span></span></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>这个题目很早之前便开始在脑子里转了，之后陆陆续续又有很多零碎的想法，却一直没有整理。最近离开了忙了2年的创业公司，下个工作又不知何时开始，于是整理之前的诸多想法。此篇便是之一</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">开篇</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>本篇猜想基于当下互联网上这样一个大环境：你是不是有这样的经历，在google上搜索某个软件的下载地址、电影的bt种子或者连续剧的e2k链接地址，结果列表里有不少论坛的链接，点进去，发现是篇帖子，所需链接被大号、加粗甚至大红大绿进行修饰。刚欣喜若狂地试图点击“下载”，却被提示“本贴所包含附件需要登录才能显示”，或者“附件需要回复本贴才能看见”。于是郁闷地开始注册，便更无奈地发现经常在坛子里使用的ID却“已被注册”或者“不可用”……好吧，加个后缀，jayxu2011怎么样？于是，我注册了一堆类似jayxu2010、mustangxu2009、ijay_2011的用户名，麻烦，而且只会使用一次……</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>随着互联网用户的爆炸性增长，以及越来越多的“老字号”网站（年头很久，比如google、gmail、搜狐、新浪等，<span style="background-color: #99ccff;">（i）</span>）；或者用户粘性很强的sns网站（比如facebook、twitter、youtube等，<span style="background-color: #99ccff;">（ii）</span>）；或者gtalk、msn、kik等和手机号一样用户名需要稳定的im工具<span style="background-color: #99ccff;">（iii）</span>的大量兴起，这种用户名冲突的情况会越来越严重<span style="background-color: #99ccff;">（I）</span>。 &nbsp;我们应该能算上（国内）互联网的第二代，对于只使用telnet泡泡有限坛子的老一代来说，第一我们数量极大，第二我们每个人注册的坛子、网站、im数量也极多（平均每人10个的估计，不算夸张吧），第三我们“很年轻”，80后为主，只要没有飞来横祸，在网上泡到70岁，不算过分吧，那还有半个世纪。于是将（I）往极端情况推一下：10年、20年甚至50年后，互联网上的ID注册会是一个什么情况<span style="background-color: #99ccff;">（II）</span>？再激进些，等我们这代人都入土了，互联网上的ID又会是个什么情况<span style="background-color: #99ccff;">（III）</span>？那等到90后、00后、10后……都入土了呢<span style="background-color: #99ccff;">（IV）</span>？ 上述III、IV便是此篇猜想的前提之一，虽然大过年的说这个有些不吉利，但是我只是做个半科学猜想，不是么？当然了，前提之二，就是这个猜想暂时只限于上述i、ii及iii，对于那些开了若干年便挂掉的还没我们活得久的网站，不在猜想范围之内。于是，隆重推出以下猜想：</p>
<!-- /wp:paragraph -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><!-- wp:paragraph -->
<p>对于i、ii、iii中所描述的网站，在网站存活期间，会有持续的、呈（爆炸性）增长势头的用户进行注册。虽然用户名的集合可以由ascii码排列组合后得到的集合进行真包含，但是，“有意义的”、“用户所欲的”、“延续性的”（即可以让朋友们看到后即刻联想到“我”的用户名。比如朋友们在一个陌生的网站看到一个用户叫“jayxu”，可能会上前打个招呼，看看是不是真的是“我”）用户名将会越来越少。随着时间的推移，使用诸如“jayxu_2011”的“次级”（以用户所欲的“主级”用户名作为词根，使用前后缀等手段进行退而求其次的唯一性区分的）用户名将会越来越多，如何让用户根据意愿选择“有意义的”、“用户所欲的”、“延续性的”用户名<span style="background-color: #99ccff;">（a）</span>？另一方面，当拥有某个用户名的用户从现实生活中消失（比如死亡）后，这些用户名（死号）及其所关联的数据该如何处理<span style="background-color: #99ccff;">（c）</span>？当然，（c）的前提，另一个棘手的问题是，由谁，根据什么来判定一个用户名是“死号”<span style="background-color: #99ccff;">（b）</span>？</p>
<!-- /wp:paragraph --></blockquote>
<!-- /wp:quote -->

<!-- wp:heading -->
<h2 class="wp-block-heading">破题</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading">（a）“有意义”、“用户所欲”、“延续性”</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>如上所述，对于用户来说，当在一个注册系统（包含上述i、ii、iii，下同）新注册时，首先关心的肯定是“我想要的用户名能不能被注册”，那什么是“我想要”的呢？受有关QQ号的论述，我觉得包括但不限于以下特征：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>延续性。所谓延续性是指让朋友们看见之后3秒内便能觉得“应该跟我有关系”的ID，这种延续性不光是从现实生活带来的延续性，也可以是从其它虚拟生活中产生的延续性<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>与现实生活有关联的现实延续性，比如“jayxu”，或</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>与我之前已有的其它ID有关联的虚拟延续性，比如另一个我比较常用的ID “mustang”或“mustangxu”</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list --></li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>好记。这点和“有意义”很有关系，这也是为什么我觉得本猜想不该包含诸如QQ号这类纯数字的ID的原因</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>当然，一个既有延续性又有意义的用户名八成是我所欲的了</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>延续性这个概念是相对的。因为延续性是基于我与朋友之间的某种不成文的、慢慢形成的契约而建立起来的，比如jayxu。其实比起jayxu来，我更prefer “jay”。但是，如大家所预料，想在上述i、ii、iii注册系统上注册“jay”已经是一个梦想，于是在各个坛子上注册时我都不会去考虑jay而是直接去尝试jayxu。更好的例子是这个域名，jayxu.com。久而久之，大家看到jayxu就会与我关联了。当然，这种“久而久之”是可以发生改变的，只要身边的朋友圈子也相对延续。比如大学开始的朋友会习惯于mustangxu，以及之后到jayxu的转变，而之后的朋友便只能习惯jayxu了。更极端的，可能只有极少数的朋友还有印象，很早之前，我曾经用过“sandy_xu”，比如china pub上的用户名</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>由于延续性这一概念是需要慢慢培养的，不妨设这个培养过程是一个ID序列{a0, a1, a2, ... , an, b0, b1, b2, ... , bn}，其中的“b”可以认为是一种可以被接受的，之后仅需要相对较短时间就可以完成培养的跳跃，比如从mustangxu到jayxu。而对于a0、b0的选择是整个猜想的一个重点。在上面描述的这样一个互联网的大环境中，一个刚接触互联网的“菜鸟”对于自己第一个ID a0，会遇到越来越多的冲突。比如我，发现jay肯定是个极易冲突的ID，于是我将b0定成了jayxu。然而不幸的是，由于jayxu这个坑就这么被我占了，对于之后想要使用jayxu的用户，会出现下面几种选择：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>在此系统中使用诸如jayxu2011的ID退而求其次，但仍然保持自己的ID序列稳定，在其它网站注册时，先尝试注册jayxu，如果不行依然被占坑，继续求其次（有点像线性哈希算法……）</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>为了避免以后的麻烦，直接将a0定为诸如jayxu_007相对有意义但是又不易冲突的ID。这看似解决了问题，但是，若干十年甚至若干世纪后，只要之前这些死号不被销毁，这种退而求其次的ID将会越来越长越来越多，继而会产生越来越严重的副作用。比如，目前我的朋友偶尔看见jayxu_007这个ID，根据序列{b0, b1, ...}可能会猜测是我的ID，而这种猜测可以被看做一种相对弱化的延续性。但在将来，当jayxu_007成为其它用户的a0，再加上整个系统中充斥着大量其它的jayxu_xxx时，那这种延续性就彻底被打断了：“jayxu_2012？应该是另外一个倒霉蛋吧”</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong><span style="text-decoration: underline;">我觉得究其原因，互联网和现实生活不一样，没有“代”的概念，互联网ID不会自然消亡！这该如何解决？</span></strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>按上述“算法”出现的另一个问题是，当不同用户在不同的注册系统上使用相同的词根已经培养起来相对稳定的圈子后，当这两个甚至更多个用户在某个注册系统上出现冲突时，该如何解决？按照我们目前已有的思维，谁先注册谁得利。但是对于后注册遇到冲突于是退而求其次的用户，这样公平么？尤其是诸如域名这种全球唯一却又不会消亡的注册系统，对于其它“jayxu”，这样公平么？这个问题貌似已经上升到了人文关怀的层次，我不知道该如何回答</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>这里需要提一句的是，目前已有一类技术可以解决一个现实“人”在不同注册系统拥有大量虚拟用户名的问题，就是以open id为首的各类跨站connect，比如国外的google account、facebook account、twitter account，国内的人人连接、开心连接、新浪微博连接等。这类技术的详细信息以及究竟能不能（彻底）解决上面这个问题，不在本文讨论之列</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading">（b）由谁，根据什么来判定一个用户名是“死号”</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>如上所述，互联网没有“代”的概念，那意味着，注册系统中的ID将会越攒越多，相对应的，可用的ID便会越来越少；再加上如果这个系统类似gmail，每个ID下又有数量为（保守估计）1G的数据，那若干现实代后，如果这些ID继续保留，相对于ID被占坑，保留、维护遗留数据而产生的服务器、带宽、电力消耗才更为恐怖。换句话说，相当不低碳！那这些坑能被回收利用么？俗话说一个萝卜一个坑，要想重复使用已经被占了的坑，唯一可想到的办法就是先挖掉坑里的萝卜。但是如果这位萝卜还会来使用这个ID，强行挖掉显然是不合情不合理的，除非：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>和手机号一样，如果欠费一段时间后运营商有权利回收号码并重新出售<br>但是互联网上免费的午餐太多了，除了腾讯、域名出售这样霸道且有收费系统的公司，没有运营商会使用上述这样简单粗暴的手段。那只能使用一些不粗暴的手段了，比如：
<p>&nbsp;</p><!-- wp:list -->
<ul><!-- wp:list-item -->
<li>按照注册时间，定义一个阈值，比如注册超过150年（但有可能，在这150年内原用户已经私下将帐号转交其他人使用了，如何甄别？）</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>结合实名制，进行身份证绑定，身份证失效时（我怎么觉得我有点成为了推行实名制的的帮凶？……）</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>连续不活跃时间超过一个阈值，比如10年（可能遇到与第一点相同的问题，比如10年后的某天我儿子在整理我的遗物时发现我很有情调地将当初我和他妈的sns帐号密码留给了他，刚欣喜若狂地想去看看我们当年如何在网上高调腻味，却被低调告知“账户已停用”，或者早已易主，出现“用户名或密码错”）</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>由家属告知此人已消失（没有这么有公德心的家属吧，更何况如何甄别消息的真假？家属又如何知道此人注册了多少系统？）</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>由公安机关介入、配合（算了吧，我们纳的税已经不够用了）</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list --></li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading">（c）如何处理死号及其所关联的数据</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>我经常开玩笑说，我们这代人是幸运的，因为将来等我们的孩子懂事后，我们可以有大量的数字化的信息与他们分享：爸妈谈恋爱的邮件、聊天记录、开心网上的朋友们评论、博客、微博、相册……记录了我们生活的点点滴滴，甚至可以传给我们的孙辈、曾孙辈看。但是如上所述，幸福的背后带来的却是一个恐怖的问号：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><span style="text-decoration: underline;"><strong>如果一个注册系统上的ID可以被顺利地认为是死号后，其关联的数据如何处理？</strong></span></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>呃……没觉着恐怖？那如果你是某个网站（比如开心）的运营方，现在看见每天有源源不断的新用户注册，网站上留言、照片、状态、分享、视频等各种活动进行得火热，你肯定每天坐在办公室乐滋滋地等着VC的美刀。但到2211年，如果网站还没死，上面又存着三代人几亿的ID，其中明明有1亿用户年龄已经超过了150岁，肯定早已投胎，但是他们的数据又在服务器的磁盘上（假设那时候还用磁盘吧），极少有孝顺的、知道用户名密码的子孙们上来翻翻爷爷奶奶年轻时甜言蜜语，却每天吞噬着你几十万的电费，到那时你应该会哭得很难看。摆在你面前有两条路：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>按照（b）所述找出死号，删除。（但如果我很有先见之明地把我的儿子培养成著名律师或者著名律师他爸，而且很不幸地，那时的中国已经成为法制社会并且有了集体诉讼这么一说，那昂贵的诉讼费和赔偿费肯定会让你立马打消这个念头）</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>开放一个服务，可以让子孙们在提供“相关证明”的前提下导出所有数据，然后删除。而这样会催生以下几种情况发生：<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>“导出数字信息太冷冰冰了吧，要不要制作成相册、名言警句书签之类的实体物品？这样更有纪念价值，也更加看得见摸的着啊～～”于是出现了一个新兴的行业，暂且划归在丧葬服务业下吧……</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>你爷爷有小号？多少个小号？不知道？你爷爷的！</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>你说这个账户是你爷爷的，但是没有相关证明？咱们还是打官司吧……</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>你好，这里是支付宝。你说这个帐号是你爸爸的？里面还有10w人民币，什么，你说你想继承？……</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list --></li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>更多情况下，我们这些爷爷奶奶的帐号肯定是无人来认领，那你打算怎么办？</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>很明显地，除了新开设一个收费行业看着比较靠谱且利国利民之外，上述情景中的其它问题都相当棘手，且存在着与法律相关的问题：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>上述判定一个ID是死号已经很让人抓狂了，那这里谁来开“相关证明”证明这个ID是你爷爷的呢？</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>如果发现盗领，冒名等情况，如何处理？谁负责任？</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>类似支付宝、QQ币、点卡这种虚拟货币，可以被继承么？算遗产么？</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>如果帐号存在纠纷，比如支付宝欠着别人钱，或者还没发货，那这些遗留纠纷该如何处理？</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>如果是国外的系统，是不是涉及到国际法律？</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>……</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>上面这些问题，算是本猜想的副产品吧。我不是搞法律的，亦不知如何回答</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>上述为处理ID相关数据的猜想，那ID本身呢？答案貌似是显而易见的：“重新开放注册”。那我又有问题了：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>如果上述的遗留问题没有处理干净，新注册的用户岂不是会很麻烦？就像买了回收后重新出售的手机号一样，得不停地解释：“不好意思，我不是原来的用户，他还没来得及发给你的充气娃娃我不负责补发”</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>现在的互联网正向真正的“net”发展，每个人在不同注册系统间会有错综复杂的关联关系，比如在博客上放了到自己相册、开心、微博等等的链接，如果其中某个链接被服务商回收，剩下的关联链接如何处理？如果哪天我老婆正兴高采烈地浏览我新买的域名下的博客，发现有个flickr的链接和该域名相关，而那个flickr里存放了之前那个老顽童存了半辈子的违禁照片，我怎么向我老婆解释？“老婆，你看，这显然不可能是我的相册，这些造型都是半个世纪前的潮流了，我现在看了就恶心”……</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>另一块可能出现问题的是类似google这些搜索引擎，或者更精确地说，是那些布满整个互联网的蜘蛛，仅靠它们的智商怎么判断两个原先属于同一个现实人互相关联的链接现在已经是不同用户的私产了？</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 class="wp-block-heading">结语</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>此篇酝酿了很久，整理、行文又花了两天，我本不指望能解决什么问题，只是抛出了一堆在我脑海萦绕了很久的砖，有没有玉和之，我亦无指望。但愿这些只是我的杞人忧天，因为是不是真的能有互联网系统成为百年老字号，本身就是个猜想。但如果真的有一天全世界遇到了这些问题，希望我是第一个将此整理并公开发布的人。如果有这份荣幸，希望此猜想命名为“jayxu猜想”，如果大家心情好打算给我个图灵奖玩玩，我也会厚着脸皮揣入囊中</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>最后再啰嗦一句，如果有人对此文有兴趣，打算转载、充实、发展甚至翻译成其它诸国语言，我不会吝啬，只是希望，注上原文出处并告知，多谢！</p>
<!-- /wp:paragraph -->