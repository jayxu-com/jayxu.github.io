---
id: 15980
title: '［ISUX译］Touch bar 设计指南 [zz]'
date: '2016-11-07T17:04:06+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15980'
permalink: /2016/11/07/15980
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '4229'
dsq_thread_id:
    - '5284949192'
image: 'https://d1k8eqsfs47rrv.cloudfront.net/log/wp-content/uploads/2016/11/022208-7303.png'
---

原文转自：<a href="https://isux.tencent.com/touchbar_guideline.html" target="_blank">腾讯ISUX</a>

<hr />

导语：日前苹果发布会上，最大的亮点之一当属替代一栏功能键的Touch bar。本文包括有5个小节，详细介绍了Touch bar设计原则、新特性和基本元素 ，一起来学习。
<div>
<h2>Touch bar概述</h2>
</div>
<div>

Touch Bar是位于新一代MacBook Pro键盘上方的一条 Retina 显示屏，同时也是与主屏幕内容交互提供动态操作界面的输入设备。基于当前语境，Touch Bar的这些控件能对系统或应用的功能进行快速访问。 例如，当用户在编辑文档时，Touch Bar可提供调整字体类型和大小的控件。 当用户查看地图时，Touch Bar可一键快速查找位置附近的加油站、住宿和餐馆。 Touch Bar右侧的Touch ID传感器支持指纹登录计算机及App Store和Apple Pay的购买支付功能。

&nbsp;

</div>
<img class="alignnone size-medium wp-image-23324" src="https://isux.tencent.com/wp-content/uploads/2016/11/022208-7303-590x274.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022208-7303-590x274.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022208-7303-768x357.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022208-7303-630x293.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022208-7303-770x358.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022208-7303-310x144.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022208-7303.png 1360w" alt="touchbar" width="590" height="274" />

&nbsp;

默认情况下，位于Touch Bar右侧的可扩展控件条（Control Strip）中包含了系统级操作的控件，如唤起Siri、调整主屏幕的亮度及音量等。而在此之前，用户是通过物理按键进行大多数的此类操作。你可以在位于控件条左侧的应用程序区域中，写入特定的应用控件。Esc（退出键）或其他系统按键会根据当前情况出现在应用区域的左侧。

<img class="alignnone size-medium wp-image-23325" src="https://isux.tencent.com/wp-content/uploads/2016/11/022210-30162-590x76.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022210-30162-590x76.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022210-30162-768x99.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022210-30162-630x81.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022210-30162-770x99.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022210-30162-310x40.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022210-30162.png 1360w" alt="2" width="590" height="76" />

Touch Bar是可配置的。用户可以从控件条中移除功能，甚至将其完全隐藏。在隐藏状态下，仅显示应用控件。用户也可以隐藏应用程序区域，只显示扩展的控制条。有些应用也允许用户在应用区域中添加或删除操作。

若要在应用中以代码实现Touch Bar功能，请参阅 NSTouchBar的参考文档 。若想了解如何使用Xcode中的Interface Builder将Touch Bar控件添加到应用程序，请参阅 Xcode Help。
<h3>为Touch Bar设计</h3>
在设计Touch Bar应用界面时，请遵循以下规范：

<strong>设计情景化体验。</strong>Touch Bar内容需与主屏幕当前内容相关。在应用程序中区分不同的场景，并根据应用程序的实际使用情况，思考如何曝光不同层级的功能。

<strong>将Touch Bar看作键盘和触控板的延伸，而非显示器。</strong>尽管在技术层面上Touch Bar就是屏幕，但它是被视作输入设备使用的，而非辅助显示器。用户可能会通过Touch Bar来定位或使用某个功能，但他们的焦点应该处于主屏幕之上。任何过分吸引用户注意力或者会影响主屏幕上首页任务的信息，如警告窗口、信息、滚动内容、静态内容等，都不应该在Touch Bar上展示。

<strong>视觉效果尽量与实体键盘一致。</strong>Touch Bar中的控件在大小和颜色方面应尽可能与实体键盘外观保持一致。

<strong>不要单独地在Touch Bar中显示某项功能。</strong>并非所有设备都有Touch Bar，用户也有可能选择禁用一个应用程序配置在Touch bar上的控件。应该始终提供能在键盘或触控板上执行任务的方式。

<strong>控件应能立即生效。</strong>提供更快捷的操作，否则用户需要用更多步骤来完成诸如点击控件或从菜单选取项目这样的任务。具体可查看Controls.

<strong>立即响应用户操作。</strong>即便应用在工作中或主屏幕正更新内容，Touch Bar中的任何已启用的控件也应能立即响应用户的操作。

<strong>尽可能让在Touch Bar中启动的任务，在Touch Bar中完成。</strong>用户不应该切换到键盘或触控板来完成任务，除非这项任务所要求的界面控件的复杂度超出了Touch Bar的支持范围。

<strong>避免使用Touch Bar执行常见的快捷键任务。</strong>一般来说，Touch Bar不提供包含查找、全选、取消选择、复制、剪切、粘贴、撤消、重做、新建、保存、关闭、打印和退出等操作，也不应该重复提供已有的键位导航，如向上翻页和向下翻页。

<strong>一致并准确地反映状态。</strong>如果控件同时处于Touch Bar和主屏幕之上，两处应呈现相同的状态。例如，如果一个按钮在主屏幕上是禁用状态，那么它在Touch Bar中也应为禁用状态。

<strong>避免将Touch Bar上的交互行为镜像显示到主屏幕上。</strong>例如，如果用户在Touch Bar中点击了按钮并显示了其选项列表，这些选项不应在主屏幕上显示。
<h2 id="interaction">1 交互</h2>
<h3>1.1 辅助功能</h3>
macOS提供了大量的辅助功能来帮助失明、失聪以及其他残疾群体。与标准界面元素一样，Touch Bar中的控件也可以轻松访问。

<strong>为控件提供替代文本标签。</strong>文本标签并不会显示在触控栏上，但是它们能让VoiceOver语音描述控件，让视力障碍用户的调用和导航操作更轻松。

<strong>为自定义控件添加文本标签。</strong>VoiceOver可以借用这些标签，语音描述自定义屏幕上的控件。相关指引，请参阅Customization。
<h3>1.2 用户自定义</h3>
Touch Bar上的应用控件都允许用户添加、删除或重新排列，以满足其各自的工作方式。

<strong>通常来说，允许用户自定义。</strong>你无法预期用户会如何使用你的应用。为重要和常用的功能提供默认值，但允许用户自主调整以满足自己需要。
<h3>1.3 全屏和聚焦内容的应用</h3>
全屏模式的应用提供了无干扰工作环境。在全屏模式下，工具栏和其他控件通常是隐藏的，只有在用户调用它们时才显示，比如将指针移动到屏幕顶部。为了让用户聚焦内容，一些应用也会在主屏幕上隐藏控件，例如，用户用QuickTime播放电影或以幻灯片的方式查看照片时。通过在Touch bar中显示控件，用户可以直接访问常用功能，而无需移动指针或查看叠加在其内容上的控件。

<strong>提供相关和常用的控件。</strong>当控件在主屏幕上隐藏时，Touch bar可能只包含可见控件，所以这些控件应该对用户在主屏幕看到的内容有用和相关。
<h3><strong>1.4 手势操作</strong></h3>
用户通过使用以下手势来与Touch Bar交互：

<strong>点击。</strong>激活控件，例如按钮。选择对象，例如表情符号，颜色或分段控件。

<strong>长按。</strong>激活控件下一层级操作，比如按钮。例如当邮件处于激活状态时点击“标记”按钮可以增加标记，触摸并按住标记按钮会展开操作浮层，让你选择标记的颜色。长按标记按钮会展开操作浮层，让你选择标记的颜色。

<strong>水平滑动（平移）。</strong>可以移动对象，比如将滑块从一侧移动到另一侧。可以快速浏览内容，比如通过滚轴查看日期或照片。

<strong>多点触控。</strong>虽然Touch Bar可以响应多个手指的触控，例如捏合手势，但多点触控手势可能会造成麻烦，应该谨慎使用。
<h2 id="visual"><strong>2 视觉设计</strong></h2>
<h3><strong>2.1 动画</strong></h3>
<strong>避免动画。</strong> Touch Bar是键盘的延伸，用户对键盘中出现动画没有预期。 此外，过度或不必要的动画让用户分心。
<h3><strong>2.2 颜色</strong></h3>
mac OS定义了一系列系统颜色，可以动态地匹配标准界面控件的配色方案，如按钮和标签。以下系统颜色是Touch Bar的理想选择：
<ul>
 	<li>控件颜色</li>
 	<li>标签颜色</li>
 	<li>二级标签颜色</li>
 	<li>三级标签颜色</li>
 	<li> 四级标签颜色</li>
</ul>
系统颜色会基于环境光和键盘背光的亮度等因素，自动地响应系统白点变化。

要了解在应用程序中使用系统颜色，请参阅NSColor的参考文档。

<strong>优先使用标准控件和系统图标。</strong>标准控件和系统图标的用色已很好的适用于Touch Bar。有关可用系统图标的列表，请参阅Icons.

<strong>少而精地使用颜色。</strong>一般来说，Touch Bar的外观应与实体键盘类似。 单色效果更好。如果必须使用多种颜色，请确保美观，且主要在临时状态下使用。不要使用太多或不恰当的颜色。

<img class="alignnone size-medium wp-image-23326" src="https://isux.tencent.com/wp-content/uploads/2016/11/022212-41427-590x22.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022212-41427-590x22.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022212-41427-768x28.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022212-41427-630x23.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022212-41427-770x28.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022212-41427-310x11.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022212-41427.png 1360w" alt="3" width="590" height="22" />

<strong>用颜色凸显信息。</strong>颜色可以让重要控件更显眼。默认控件使用蓝色，不可逆操作控件使用红色。

选择与应用相符的有限色板。巧妙地使用颜色是一个传达品牌的好办法。

<img class="alignnone size-medium wp-image-23327" src="https://isux.tencent.com/wp-content/uploads/2016/11/022213-27336-590x22.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022213-27336-590x22.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022213-27336-768x28.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022213-27336-630x23.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022213-27336-770x28.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022213-27336-310x11.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022213-27336.png 1360w" alt="4" width="590" height="22" />

<strong>提供宽色域的设计稿。</strong> Touch Bar支持P3颜色空间，可以产生比sRGB更丰富，更饱和的颜色。 使用显示P3颜色配置文件，每像素16位（每通道），并以.png格式导出设计稿。
<h3><strong>2.3 布局</strong></h3>
除开Touch ID传感器，Touch Bar大小为2170x60px。Touch Bar采用的高分辨率Renita屏 ，换算为对应的pt值为1085x30pt。

<img class="alignnone size-medium wp-image-23328" src="https://isux.tencent.com/wp-content/uploads/2016/11/022214-56115-590x22.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022214-56115-590x22.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022214-56115-768x28.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022214-56115-630x23.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022214-56115-770x28.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022214-56115-310x11.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022214-56115.png 1360w" alt="5" width="590" height="22" />
<h4>2.3.1 Touch Bar区域</h4>
在其标准配置中，Touch Bar包含三个主要区域，每个区域的间隔是32px。

<img class="alignnone size-medium wp-image-23360" src="https://isux.tencent.com/wp-content/uploads/2016/11/052122-9749-590x242.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/052122-9749-590x242.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/052122-9749-768x315.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/052122-9749-630x259.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/052122-9749-770x316.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/052122-9749-310x127.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/052122-9749.png 1004w" alt="2016-11-03-xiawu1-20-55" width="590" height="242" />

设计时假设默认控件条可见。 虽然用户可以重新配置控件条，减小它的大小，并完全禁用它，但你的应用程序不应该依赖这个控制条。
<h4>2.3.2 放置应用控件</h4>
在Touch Bar中，系统提供了几个选项来分隔app控件：

<strong><img class="size-medium wp-image-23358 aligncenter" src="https://isux.tencent.com/wp-content/uploads/2016/11/051505-99819-590x404.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/051505-99819-590x404.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/051505-99819-630x432.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/051505-99819-310x212.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/051505-99819.png 705w" alt="pingmukuaizhao-2016-11-03-xiawu1-14-39" width="590" height="404" /></strong>

<strong>合乎逻辑、直观地摆放控件。</strong> 应用程序区域的左侧适用于通用控件。 例如，当Notes处于激活态时，无论是在浏览笔记、编辑笔记还是在浏览附件，都会在Touch Bar的最左侧显示用于添加注释的“撰写”按钮。 否则，最好中间位置放置主要控件，左侧放置二级选项。

<strong>构建灵活的布局。</strong> 应用程序区域的宽度会根据控件条的配置而有所不同，所以在有可用空间的时候，考虑用滑块、滑动条这些控件延展操作区域。

<strong>尽量保持一致的间距。</strong> Touch Bar中的控件间距尽可能相等，除非有让内容变清晰或归类相关控件的需要，才改变间距。

<strong>用灵活的间距和分组辅助对齐。</strong> 控件之间灵活的间距将左侧控件推向Touch Bar左侧，将右侧控件推向Touch Bar右侧。分组让你可以一次放置多个控件。通过标记控件或者控件组，你可以使其作为主要控件区在Touch Bar居中。

<strong>不要自动改变控件位置。</strong> 随意改变控件位置，用户会感到受挫和困惑。 用户可以手动自定义控件位置，但你的应用应避免无缘无故改变位置的情况。

<strong>不要反过来从右至左地放置控件。</strong>反置控件可能会导致Touch Bar自定义功能出现问题，并且系统已经反置了某些控件，例如分段控件和滑块。
<h4>2.3.3 常见布局</h4>
由于存在多种配置选项和控件大小设置，对于不同的app，Touch Bar中的布局样式可以多种多样，但是尽可能的使用常见的布局样式。

<strong>流体布局。</strong> 此布局包含大小一致的控件，如按钮。

<img class="alignnone size-medium wp-image-23330" src="https://isux.tencent.com/wp-content/uploads/2016/11/022215-17207-590x83.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022215-17207-590x83.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022215-17207-768x108.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022215-17207-630x89.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022215-17207-770x108.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022215-17207-310x44.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022215-17207.png 1380w" alt="7" width="590" height="83" />

<img class="alignnone size-medium wp-image-23331" src="https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-590x83.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-590x83.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-768x108.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-630x89.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-770x108.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-310x44.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499.png 1380w" alt="8" width="590" height="83" />

<strong>有一个主要控件区的布局。</strong> Touch Bar的中心包含单个大型控件，例如候选列表（在文本输入期间提供自动完成建议）。 其他控件（如按钮和分段控件）位于左侧。

<img class="alignnone size-medium wp-image-23331" src="https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-590x83.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-590x83.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-768x108.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-630x89.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-770x108.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-310x44.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499.png 1380w" alt="8" width="590" height="83" />
<div>

<strong>有两个主要控件区的布局。</strong> Touch Bar的中心包含两个一致大小的控件。 其他控件位于左侧。

<img class="alignnone size-medium wp-image-23331" src="https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-590x83.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-590x83.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-768x108.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-630x89.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-770x108.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499-310x44.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022216-79499.png 1380w" alt="8" width="590" height="83" />

<strong>有三个主要控件区的布局。</strong> Touch Bar的中心包含三个一致大小的控件。 其他控件位于左侧。

<img class="alignnone size-medium wp-image-23333" src="https://isux.tencent.com/wp-content/uploads/2016/11/022218-79791-590x83.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022218-79791-590x83.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022218-79791-768x108.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022218-79791-630x89.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022218-79791-770x108.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022218-79791-310x44.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022218-79791.png 1380w" alt="10" width="590" height="83" />
<h3>2.4 字体</h3>
Touch Bar使用的是macOS中的系统字体——San Francisco。 此字体针对易读性、清晰度和一致性进行了优化。 它也匹配实体键盘的字体。 标准Touch Bar控件（如按钮和分段控件）自动使用此字体。 要了解如何在应用中应用系统字体，请参阅NSFont的参考文档。
<h2 id="icon">3 图标</h2>
<h3>3.1 图形尺寸和分辨率</h3>
Touch Bar上的图片资源全部采用@2x切图。在@2x的图片中，1pt等同于2px。比如，36X36px的图标会转化为18X18pt。在图片名称后面加上@2x，然后把它们置入到Xcode文件中的@2x目录下。
<h3>3.2 自定义图标</h3>
如果系统默认图标无法满足应用内多个任务与状态，可以绘制你的专属图标。

<strong>设计高识别度的图标。</strong>图标应该与主屏幕上的应用匹配，但需要符合Touch Bar的样式风格。

<strong>让图标更简洁。</strong>太多细节会让图标语义不清，降低可读性。高拟物的图形需要简化保留最基本的元素。好的图标是通过外形轮廓表意的，只会有少量内部细节。消除锯齿以确保图标轮廓清晰。不要使用投影或用阴影与高光的方式让图标凸显出来。

<strong>让图标更一致。</strong>无论使用自定义图标还是与系统图标混合使用，所有的图标都需要通过一致的尺寸，细节，透视和描边保持相同的视觉感受。

<strong>参考系统图标设计。</strong>设计自定义图标时请参考系统图标，尽量遵循相似的表现形式。

<strong>为图标准备模板资源。</strong>图标模板是一个背景透明并有alpha通道的黑色图像。当图标显示在Touch Bar时，系统自动转化图标并为其应用适当的颜色。

<strong>测试图标。</strong>为了非常准确的判断图标的表现，需要结合场景预览所有图标，确保模板资源在被系统转化后符合预期。
<h4>3.2.1 尺寸</h4>
虽然图标可以撑满Touch Bar的高度，但图标的高度通常不超过44px（圆形图标36px）。

<img class="size-medium wp-image-23359 aligncenter" src="https://isux.tencent.com/wp-content/uploads/2016/11/051506-98059.png" sizes="(max-width: 565px) 100vw, 565px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/051506-98059.png 565w, https://isux.tencent.com/wp-content/uploads/2016/11/051506-98059-310x112.png 310w" alt="pingmukuaizhao-2016-11-03-xiawu1-14-49" width="565" height="204" /><img class="size-medium wp-image-23334 aligncenter" src="https://isux.tencent.com/wp-content/uploads/2016/11/022220-52155-590x132.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022220-52155-590x132.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022220-52155-768x172.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022220-52155-630x141.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022220-52155-770x173.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022220-52155-310x69.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022220-52155.png 1232w" alt="11" width="590" height="132" />

<strong>保持图标视觉居中。</strong>裁剪设计稿以匹配图标宽度，必要时增加内边距以确保图标在控件上显示时视觉居中。

<strong>倾斜图标尽量采用45度角。</strong>在系统图标里，倾斜元素常常会呈现45度角，例如：全屏和退出全屏的箭头图标；返回、向下、前进、向上的人字形图标；静音图标的斜线；编辑图标中的铅笔；浏览器图标中的指南针指针。查看系统提供的图标作为参考。
<h4>3.2.2 颜色和填充</h4>
Touch Bar上的图标应看上去与实体键盘按键的字形相似。如果使用了模板和系统颜色，图标会自动产生这种效果。

<strong>不要用颜色区分开关状态。</strong>系统会改变背景样式表明开关状态。

<strong>尽量用100%不透明的图标。</strong>倘若为了兼顾可读性，可用不透明度70%的作为辅助。仅当需要提升可读性和平衡度的时候，使用中间色调。

相关的指引，可查看 Color。
<h4>3.2.3 描边</h4>
为了匹配实体键盘的风格，图标尽量用2px的描边。如果需要让图标占据更多视觉重量，可以尝试3px。
<h4>3.2.4 转角</h4>
为了匹配系统图标的风格，直角图标使用2px的描边，圆角图标使用1px半径3px的描边，填充形状的圆角使用4px半径。
<h4>3.2.5 模板</h4>
使用Photoshop和Sketch模板设计合适尺寸的Touch Bar图标。下载图标模版Download Icon Templates。
<h4>3.2.6 系统提供的图标</h4>
系统提供了充足的代表常规任务和内容类型的图标，可用于应用的控件上。

<strong>尽量使用系统图标，因为它们更常见。</strong>由于系统图标是模板资源，它们能自动地填色，基于环境光和键盘背光的亮度响应系统白点变化，并对用户的交互行为自动作出反应。

<strong>不要重新定义系统图标。</strong>为确保体验的一致性，请按照图标的原本意图使用图标。比如，不要把“移动文件”图标应用于下载操作，要用原本的下载图标。

<strong>仅使用为Touch Bar而设计的系统图标。</strong>其他类型的系统图标，比如工具栏，不是为了用于Touch Bar上而设计的。
<div>

备注：

一些系统图标会在自右向左的文本场景下自动转换方向，比如前进与后退。（译者注：像波斯语、阿拉伯语、希伯来语这些语言的书写和阅读习惯都是从右向左，所以排版也要求是从右向左）

</div>
链接：<a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/Icons.html#//apple_ref/doc/uid/20000957-CH107-SW4" target="_blank">Touch Bar上的图标</a>
<h2 id="control">4 控件</h2>
系统为Touch Bar的应用区域内置了多种标准控件。尽可能地使用这些控件，以达到最佳的体验一致性。
<h3>4.1 按钮（Buttons）</h3>
点按按钮以触发应用程序的对应事件。按钮可包含图标和标题。

<img class="alignnone size-medium wp-image-23335" src="https://isux.tencent.com/wp-content/uploads/2016/11/022222-15731-590x65.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022222-15731-590x65.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022222-15731-768x84.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022222-15731-630x69.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022222-15731-770x84.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022222-15731-310x34.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022222-15731.png 1360w" alt="12" width="590" height="65" />

<strong>图标优于标题。</strong>争取设计出足够清晰明了的图标，不要依赖于文本的辅助。

<strong>使用简短的标题。</strong>太长的标题会使Touch Bar显得过于拥挤。

<strong>使用美观的边框颜色。</strong>默认边框采取了和实体按键相似的外观设计。如果确实需要自定义的话，推荐使用深色的边框颜色。
<h3>4.2 切换键（Toggles ）</h3>
切换键是按钮的一种，用于“开启”和“关闭”两种状态之间的切换。

<img class="alignnone size-medium wp-image-23336" src="https://isux.tencent.com/wp-content/uploads/2016/11/022223-48240-590x63.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022223-48240-590x63.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022223-48240-768x82.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022223-48240-630x68.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022223-48240-770x83.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022223-48240-310x33.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022223-48240.png 1360w" alt="13" width="590" height="63" />

<strong>使用背景来表现当前状态。</strong>在关闭状态下，系统会自动改变按钮的背景样式，所以不需要使用颜色、文本或另外的图标来表现当前状态。

<strong>使用切换键取代单选框和复选框。</strong>如果你需要用户在两个状态当中进行选择的话，使用切换键。
<h3>4.3 候选列表（Candidate Lists）</h3>
输入文本时，候选列表提供自动文本建议。用户可以通过点击，将文本建议输入到主屏幕中激活的文本框或文本区域内。用户可以选择展开或者收起候选列表。展开的候选列表将会替代区域内的其他控件。

<img class="alignnone size-medium wp-image-23337" src="https://isux.tencent.com/wp-content/uploads/2016/11/022224-42038-590x73.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022224-42038-590x73.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022224-42038-768x95.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022224-42038-630x78.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022224-42038-770x96.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022224-42038-310x39.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022224-42038.png 1360w" alt="14" width="590" height="73" />
<h3>4.4 字符选择器（Character Pickers）</h3>
点击字符选择器时，会打开一个包含一系列特殊字符的弹出视窗，如emoji。用户可以通过点击，将其输入至主屏幕中激活的文本框或文本区域中。

<img class="alignnone size-medium wp-image-23338" src="https://isux.tencent.com/wp-content/uploads/2016/11/022226-68977-590x63.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022226-68977-590x63.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022226-68977-768x82.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022226-68977-630x67.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022226-68977-770x82.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022226-68977-310x33.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022226-68977.png 1360w" alt="15" width="590" height="63" />

<img class="alignnone size-medium wp-image-23339" src="https://isux.tencent.com/wp-content/uploads/2016/11/022228-84401-590x72.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022228-84401-590x72.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022228-84401-768x93.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022228-84401-630x76.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022228-84401-770x93.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022228-84401-310x38.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022228-84401.png 1360w" alt="16" width="590" height="72" />
<h3>4.5 拾色器（Color Pickers）</h3>
点击拾色器时，会打开一个包含了颜色选择控件的弹出视窗。拾色器可通过配置，展示为选取颜色、边框或文本颜色的图标。无论是哪种图标，所有拾色器打开后显示的均为同一视窗。

<img class="alignnone size-medium wp-image-23340" src="https://isux.tencent.com/wp-content/uploads/2016/11/022232-1214-590x99.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022232-1214-590x99.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022232-1214-768x129.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022232-1214-630x106.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022232-1214-770x130.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022232-1214-310x52.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022232-1214.png 1360w" alt="17" width="590" height="99" />

<img class="alignnone size-medium wp-image-23341" src="https://isux.tencent.com/wp-content/uploads/2016/11/022234-13299-590x71.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022234-13299-590x71.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022234-13299-768x93.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022234-13299-630x76.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022234-13299-770x93.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022234-13299-310x37.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022234-13299.png 1360w" alt="18" width="590" height="71" />

<strong>带意图地使用图标。</strong>当拾取边框颜色时，使用边框颜色选取图标。当拾取文本颜色时，使用文本颜色选取图标。其他拾色场景下，使用颜色选取图标。
<h3>4.6 标签（Labels）</h3>
标签展示只读文本，通常是为了描述一个控件而设。

<strong>一般来说，避免使用标签。</strong>虽然Touch Bar可以展示标签，但是最好不要使用，因为用户并不能与标签进行交互。我们更应该专注于为控件设计更加有趣的图标。如果你必须使用标签，使之尽可能的简短。

<strong>当需要为复杂图标做文字补充时，标题优于标签。</strong>如果一个控件的图标本身并不是足够清晰名了，可考虑增加一个简短的标题以提供其使用语境。

<img class="alignnone size-medium wp-image-23342" src="https://isux.tencent.com/wp-content/uploads/2016/11/022235-82237-590x72.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022235-82237-590x72.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022235-82237-768x94.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022235-82237-630x77.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022235-82237-770x94.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022235-82237-310x38.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022235-82237.png 1360w" alt="19" width="590" height="72" />
<h3>4.7 弹出视窗（Popovers ）</h3>
在折叠状态下，弹出视窗在Touch Bar中表现为一个单独的按钮。

<img class="alignnone size-medium wp-image-23343" src="https://isux.tencent.com/wp-content/uploads/2016/11/022236-58853-590x62.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022236-58853-590x62.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022236-58853-768x81.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022236-58853-630x67.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022236-58853-770x82.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022236-58853-310x33.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022236-58853.png 1360w" alt="20" width="590" height="62" />

展开时，弹出视窗将生成一个包含一组暂驻控件的模块，覆盖掉应用区域中的其他控件。在这个模块的覆盖下，用户必须进行选择操作，或者也可以通过点击退出键收起当前菜单，使得弹出视窗回到折叠态。

<img class="alignnone size-medium wp-image-23344" src="https://isux.tencent.com/wp-content/uploads/2016/11/022237-98554-590x71.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022237-98554-590x71.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022237-98554-768x93.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022237-98554-630x76.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022237-98554-770x93.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022237-98554-310x37.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022237-98554.png 1360w" alt="21" width="590" height="71" />

通过点击以展开弹出视窗。弹出视窗也可以按需响应长按动作。支持长按动作的弹出视窗需要包含左箭头符号。

<img class="alignnone size-medium wp-image-23345" src="https://isux.tencent.com/wp-content/uploads/2016/11/022238-38269-590x63.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022238-38269-590x63.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-38269-768x82.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-38269-630x67.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-38269-770x82.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-38269-310x33.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-38269.png 1360w" alt="22" width="590" height="63" />

通过长按触发的弹出视窗，可以使用和普通弹出视窗一样又或者是完全不同的蒙层。在长按触发的蒙层中，用户通过滑动手指到达想要的选项，松开以完成选择并关闭弹出视窗。

<img class="alignnone size-medium wp-image-23346" src="https://isux.tencent.com/wp-content/uploads/2016/11/022238-8339-590x71.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022238-8339-590x71.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-8339-768x92.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-8339-630x76.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-8339-770x92.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-8339-310x37.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022238-8339.png 1360w" alt="23" width="590" height="71" />

<strong>有节制地使用弹出视窗。</strong>单一点击应能触发Touch Bar中的大多数控件。

<strong>避免嵌套的弹出视窗。</strong>一般来说，尽量避免在Touch Bar中进行一级以上的导航。

<strong>给简单的弹出视窗们保留长按动作。</strong>长按动作主要是为了展示一组包含简单选项的蒙层而保留，例如分段控件，这样用户便可以从中进行选择。

<strong>在折叠状态的弹出视窗上表明选中项。</strong>弹出视窗在展开时包含了一组选项，在折叠状态下则应该示意当前选中项。

<strong>提供明确的退出路径。</strong>确保用户知道如何收起一个弹出视窗，并回到之前的一组控件。
<h3>4.8 滑动条（scrubber）</h3>
滑动条可以让用户通过左右滑动，在如一组时间或者照片等内容中进行概览。滑动条可以是固定的，可以是能自由移动的，也可以是高度定制化的——但是需要保留和Touch Bar相称的外观。

</div>
<div>
<div>
<h4>4.8.1 固定滑动条</h4>
</div>
固定滑动条为一组组织好的内容提供流畅而连续的交互，如Safari的标签页切换。用户在使用滑动条左右滑动时，手指底下的项目高亮展示。取决于滑动条的配置，用户可以通过滑动或抬起手指完成选择。如果内容超出了固定滑动条的显示区域，当手指滑动到控件的边缘的时候，滑动条会自动滑出并显示剩余的选项。在固定滑动条里，用户的手指直接移动的是选项，并非内容。

<img class="alignnone size-medium wp-image-23347" src="https://isux.tencent.com/wp-content/uploads/2016/11/022239-76623-590x71.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022239-76623-590x71.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022239-76623-768x93.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022239-76623-630x76.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022239-76623-770x93.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022239-76623-310x37.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022239-76623.png 1360w" alt="24" width="590" height="71" />
<h4>4.8.2 自由滑动条</h4>
自由滑动条在一个可自由滑动的列表中展示内容，例如“日历”应用中的一组日期，用户左右滑便可使直接查看内容。取决于滑动条的配置，如果一个选项处在某个特定的位置，如滑动条的中央，那么这个选项则被选中；或者滑动条本身是固定的，需要用户手动点击选择。

<img class="alignnone size-medium wp-image-23348" src="https://isux.tencent.com/wp-content/uploads/2016/11/022240-97481-590x72.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022240-97481-590x72.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022240-97481-768x93.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022240-97481-630x76.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022240-97481-770x93.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022240-97481-310x38.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022240-97481.png 1360w" alt="25" width="590" height="72" />

使用符合预期和具有组织逻辑的值。在自由滑动条中，如果可滑动列表是固定的话，则很多数值可能是被隐藏起来的。像是一组按照字母表顺序排列的国家列表一样，如果用户在使用的时候能推测出这些数值是什么最好不过，这样用户便能快速地在列表中移动。

避免展示数字过大的列表。在Touch Bar中浏览长列表非常乏味。如果你有一组数值很大的列表，考虑在主屏幕而非Touch Bar上展示，这样的话键盘或者触控板均可用作导航。
<h3>4.9 分段控件（Segmented Controls）</h3>
分段控件是由包含了两个或以上线性关系的部件所组成，每个部件的作用就像是按钮——通常会配置为切换键。在这个控件中，所有部件等宽。像按钮一样，分段控件可以包含文本和图标。

<img class="alignnone size-medium wp-image-23349" src="https://isux.tencent.com/wp-content/uploads/2016/11/022241-65017-590x70.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022241-65017-590x70.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022241-65017-768x91.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022241-65017-630x75.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022241-65017-770x91.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022241-65017-310x37.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022241-65017.png 1360w" alt="26" width="590" height="70" />

限制部件的数量以提升可用性。更宽的部件更容易点击。

图标优于标题。争取设计出足够清晰明了的图标，不要依赖于文本的辅助。

保持分段控件中的内容尺寸的一致性。因为各个部件宽度相等，如果每个部件中内容填充不一的话，会显得不够美观。

使用简短的标题。太长的标题会使Touch Bar显得过于拥挤。

深色的边框颜色变化优于浅色。默认边框采取了和实体按键相似的外观设计。如果确实需要自定义的话，推荐使用深色的边框颜色。
<h3>4.10 分享服务选择器（Sharing Service Pickers ）</h3>
分享服务选择器为用户提供了一种便捷的分享方式，用户可以分享文本、图像和应用程序、社交媒体账号中的其他内容，又或是其他服务。通过点击分享服务选择器，触发包含分享按钮的弹出视窗。

<img class="alignnone size-medium wp-image-23350" src="https://isux.tencent.com/wp-content/uploads/2016/11/022242-74538-590x64.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022242-74538-590x64.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022242-74538-768x83.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022242-74538-630x68.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022242-74538-770x83.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022242-74538-310x34.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022242-74538.png 1360w" alt="27" width="590" height="64" />

<img class="alignnone size-medium wp-image-23351" src="https://isux.tencent.com/wp-content/uploads/2016/11/022243-38054-590x72.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022243-38054-590x72.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022243-38054-768x94.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022243-38054-630x77.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022243-38054-770x95.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022243-38054-310x38.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022243-38054.png 1360w" alt="28" width="590" height="72" />

仅在有可分享的内容时激活分享服务选择器。如果用户没有选择任何文本、图像或者其他可分享内容，应该停用分享服务选择器。
<h3>4.11 滑块（Sliders ）</h3>
滑块由一个水平轨道和一个名为拇指键的控件所组成，你可以在其最大值和最小值之间滑动，例如调节屏幕的亮度或视频的播放进度。在滑块的数值改变时，拇指键和最小值之间的轨道将会被填充以颜色。

<img class="alignnone size-medium wp-image-23352" src="https://isux.tencent.com/wp-content/uploads/2016/11/022244-56983-590x72.png" sizes="(max-width: 590px) 100vw, 590px" srcset="https://isux.tencent.com/wp-content/uploads/2016/11/022244-56983-590x72.png 590w, https://isux.tencent.com/wp-content/uploads/2016/11/022244-56983-768x93.png 768w, https://isux.tencent.com/wp-content/uploads/2016/11/022244-56983-630x76.png 630w, https://isux.tencent.com/wp-content/uploads/2016/11/022244-56983-770x93.png 770w, https://isux.tencent.com/wp-content/uploads/2016/11/022244-56983-310x38.png 310w, https://isux.tencent.com/wp-content/uploads/2016/11/022244-56983.png 1360w" alt="29" width="590" height="72" />

自定义滑块的样式以适应你的应用，增添趣味。考虑让滑轨的颜色和你应用的配色相互搭配。

提供左右两边的图标以说明最大值和最小值所代表的含义。举个例子，调整图像大小的滑块可在左边配置一个小图图标，而在右边配置一个大图图标。

</div>
&nbsp;

原文访问地址：<a href="https://developer.apple.com/library/content/documentation/UserExperience/Conceptual/OSXHIGuidelines/AbouttheTouchBar.html#//apple_ref/doc/uid/20000957-CH104-SW1" target="_blank">macOS Human Interface Guidelines：About the Touch Bar</a>

翻译版PDF下载：<a href="http://share.weiyun.com/a3151a284fdad43078ef52f4fbe84e39" target="_blank">点击下载</a>