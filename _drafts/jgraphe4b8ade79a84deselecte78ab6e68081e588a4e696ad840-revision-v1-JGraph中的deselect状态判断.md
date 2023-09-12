---
id: 17384
title: JGraph中的deselect状态判断
date: '2021-02-21T19:47:04+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/?p=17384'
permalink: '/?p=17384'
---

<!-- wp:image {"id":17379,"sizeSlug":"large","linkDestination":"attachment"} -->
<figure class="wp-block-image size-large"><a href="https://www.jayxu.com/2008/11/14/840/jgrapht-logo-transparent-cropped-2"><img src="https://www.jayxu.com/log/wp-content/uploads/2021/02/jgrapht-logo-transparent-cropped-1280x709.png" alt="" class="wp-image-17379"/></a></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><a href="http://www.jgraph.com/" target="_blank" rel="noopener">JGraph</a>是基于Java swing、Java 2D开发的纯Java图形库，很像Eclipse的EMF、JMF，可以很方便地帮助开发人员在Swing框架中实现组件的呈现、布局、拖拽、group等图形化操作。JGraph也是基于MVC模式实现，将整个框架分为cell（M层）、cell view（C层）和renderer（V层）。有一些设计思想很有趣，比如它的GraphConstants，将所有属性存在传入的map里，通过方法签名实现属性的意义化和类型限制，很有趣的思想</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>下面进入正题，如何判断一个cell view被deselect。JGraph现在已半商业化，文档很稀少，JavaDoc更是不堪入目，最好的研究方法还是读源代码，比如前两天为了正确设置cell view的虚线边框颜色就看了一晚上源代码<br>JGraph的事件监听写得很诡异，在cell view中需要通过以下方法添加监听器：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">class MyCellView extends VertexView {
    public CellHandle getHandle(GraphContext context) {
        return new CellHandle(){
            void paint(Graphics g);

            void overlay(Graphics g);

            void mouseMoved(MouseEvent event);

            void mousePressed(MouseEvent event);

            void mouseDragged(MouseEvent event);

            void mouseReleased(MouseEvent event);
        };
    }
}</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>你可以通过JGraph对象的<code><code data-enlighter-language="java" class="EnlighterJSRAW">getSelectionCell()</code></code>或<code><code data-enlighter-language="java" class="EnlighterJSRAW">getSelectionCells()</code></code>获得被选中的cell，但是有一个问题，就是当你单击空白区域以取消选择一个cell view时，该方法依然返回非空的最后选择的对象。于是尝试从MouseEvent获得点击时鼠标的X、Y坐标，并调用<code><code data-enlighter-language="java" class="EnlighterJSRAW">getFirstCellForLocation(double x, double y)</code></code>获得鼠标位置的cell（没有则返回null）。但这样还是有问题，当你通过框选选择一个（或若干个）cell时，<code><code data-enlighter-language="java" class="EnlighterJSRAW">getFirstCellForLocation(double x, double y)</code></code>返回的对象取决于你实现的方法（是press、drag还是release）。最后，在通读了一下JGraph的JavaDoc后，发现可以使用如下方法解决这个问题：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">graph.getSelectionModel().addGraphSelectionListener(new GraphSelectionListener() {
    public void valueChanged(GraphSelectionEvent e) {
        MachineCell[] cell = null;

        if (e.isAddedCell()) { // selected
            cell = new MachineCell[]{(MachineCell) e.getCell()};
        } else {
            cell = new MachineCell[0];
        }

        for (ActionListener l : listeners) {
            l.actionPerformed(new ActionEvent(cell, 0, ""));
        }
    }
});</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>其中第五行的isAddedCell()方法签名如下：</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>isAddedCell</h3>
<!-- /wp:heading -->

<!-- wp:enlighter/codeblock {"language":"java","linenumbers":"false"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="java" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="false" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">public boolean isAddedCell()</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:html -->
<dl>
<dd>Returns true if the first cell has been added to the selection, a return value of false means the first cell has been removed from the selection.
<p>&nbsp;</p>
</dd>
<dd>
<dl>
<dt><strong>Returns:</strong></dt>
<dd>whether or not the first cell has been added or removed</dd>
</dl>
</dd>
</dl>
<!-- /wp:html -->