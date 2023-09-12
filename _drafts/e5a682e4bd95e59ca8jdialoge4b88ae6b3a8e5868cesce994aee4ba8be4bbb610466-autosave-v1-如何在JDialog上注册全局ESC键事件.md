---
id: 18169
title: 如何在JDialog上注册全局ESC键事件
date: '2023-01-13T00:57:32+08:00'
author: Jay
layout: revision
guid: 'https://www.jayxu.com/?p=18169'
permalink: '/?p=18169'
---

<!-- wp:paragraph -->
<p>大多数用户可能会有这么一个习惯：对于富客户端弹出的Dialog，习惯使用ESC将其关闭，而不是“叉掉它”。在Swing中，弹出窗口一般继承自JDialog类，但默认没有对ESC键事件做响应，下面这段代码可以完成这个功能：</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock {"language":"java"} -->
<pre class="EnlighterJSRAW" data-enlighter-language="java" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">private static final KeyStroke escapeStroke = KeyStroke.getKeyStroke(KeyEvent.VK_ESCAPE, 0);
public static final String dispatchWindowClosingActionMapKey = "com.jayxu:WINDOW_CLOSING"; // any key string you like

public static void installEscapeCloseOperation(final JDialog dialog) { // any method name you like
    Action dispatchClosing = new AbstractAction() {
        public void actionPerformed(ActionEvent event) {
            dialog.dispatchEvent(new WindowEvent(dialog, WindowEvent.WINDOW_CLOSING));
        }
    };

    JRootPane root = dialog.getRootPane();
    root.getInputMap(JComponent.WHEN_IN_FOCUSED_WINDOW).put(escapeStroke, dispatchWindowClosingActionMapKey);
    root.getActionMap().put( dispatchWindowClosingActionMapKey, dispatchClosing);
}</pre>
<!-- /wp:enlighter/codeblock -->