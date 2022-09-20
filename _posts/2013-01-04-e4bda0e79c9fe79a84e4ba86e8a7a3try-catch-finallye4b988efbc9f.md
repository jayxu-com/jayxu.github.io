---
id: 13643
title: 你真的了解try-catch-finally么？
date: '2013-01-04T19:22:25+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=13643'
permalink: /2013/01/04/13643
posturl_add_url:
    - 'yes'
views:
    - '3905'
duoshuo_thread_id:
    - '6.3356050859046E+18'
dsq_thread_id:
    - '4351723636'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>try-catch-finally看似是很简单的执行流程，但是如果加上return，结果你能争取判断么？考虑以下代码：</p>
<!-- /wp:paragraph -->

<!-- wp:preformatted -->
<pre lang="java" class="wp-block-preformatted">public class ExceptionTest {
    public static void main(String[] args) {
        String s = null;

        try {
            s = genString(true);
        } finally {
            System.out.println(s);
        }
    }

    private static String genString(boolean throwEx) {
        try {
            if (throwEx) {
                throw new RuntimeException("Exception");
            }

            System.out.println("in try");
            return "no exception";
        } catch (Exception ex) {
            System.out.println("in catch");
            return "exception";
        } finally {
            System.out.println("in finally");
            return "finally";
        }
    }
}</pre>
<!-- /wp:preformatted -->

<!-- wp:paragraph -->
<p>其中genString(boolean)可以决定是否抛异常，在“true”时会打印什么？或者说，genString方法究竟会执行哪条return？传入“false”呢？</p>
<!-- /wp:paragraph -->