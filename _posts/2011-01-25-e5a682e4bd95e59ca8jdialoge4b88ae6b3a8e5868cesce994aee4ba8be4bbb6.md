---
id: 10466
title: 如何在JDialog上注册全局ESC键事件
date: '2011-01-25T13:53:11+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=10466'
permalink: /2011/01/25/10466
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
dsq_thread_id:
    - '4288407198'
views:
    - '4824'
shorturl:
    - 'http://goo.gl/6AAUy'
duoshuo_thread_id:
    - '6.3356047457885E+18'
---

大多数用户可能会有这么一个习惯：对于富客户端弹出的Dialog，习惯使用ESC将其关闭，而不是“叉掉它”。在Swing中，弹出窗口一般继承自JDialog类，但默认没有对ESC键事件做响应，下面这段代码可以完成这个功能：
<pre lang="java">private static final KeyStroke escapeStroke = KeyStroke.getKeyStroke(KeyEvent.VK_ESCAPE, 0);
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