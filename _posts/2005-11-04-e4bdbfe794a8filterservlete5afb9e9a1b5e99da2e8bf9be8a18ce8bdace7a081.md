---
id: 16031
title: 使用FilterServlet对页面进行转码
date: '2005-11-04T19:42:47+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=16031'
permalink: /2005/11/04/16031
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '2097'
dsq_thread_id:
    - '5295414593'
---

相信很多朋友在使用JSP/Servlet等技术进行页面编程的时候都会或多或少地遇到乱码问题。解决的方法有很多，比较常见的是手动对所有可能包含中文的字符串进行转码：
<pre lang="java" class="">String latin = ...;
String gbk = new String(latin.getBytes("iso-8859-1"),"gbk");</pre>
这个方法过去我也比较常用，的确有效，但很累赘耶，丝毫没有模式之美，有没有更优雅的方法呢？如果你和我一样有疑虑的话，可以考虑使用FilterServlet：
<pre lang="java">import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

import org.apache.log4j.*;
 
public class CharsetFilter extends HttpServlet implements Filter{
  private static Logger logger = Logger.getLogger("Filter servlet");

  public void init(FilterConfig filterConfig) throws ServletException{
  }

  public void doFilter(ServletRequest request,ServletResponse response,FilterChain filterChain){
    if(request != null){
      String charset = request.getCharacterEncoding();
      if(charset == null || !charset.equalsIgnoreCase("gbk"))
        try{
          request.setCharacterEncoding("GBK");
        }
        catch(UnsupportedEncodingException ex){
          logger.warn(ex.getMessage());
        }
    }
    try{
      filterChain.doFilter(request,response); // 递交责任链下一环
    }
    catch(Exception ex){
      logger.error(ex.getMessage());
    }
  }

  public void destroy(){
  }
}</pre>
FilterServlet内部应该使用责任链（Chain of Responsibility）实现，在这里我们把对字符串的转码做为责任链中的一环，从上一环拿到request，处理后交给链的下一环。另外需要在web.xml里做些配置：
<pre lang="xml">
<filter>
  <filter-name>charsetfilter</filter-name>
  <filter-class>pqp.servlet.CharsetFilter</filter-class>
</filter>
<filter-mapping>
  <filter-name>charsetfilter</filter-name>
  <url-pattern>/*</url-pattern>
  <dispatcher>REQUEST</dispatcher>
</filter-mapping>
</pre>
其中“REQUEST”指定了filter拦截的类型，有REQUEST、FORWARD、ERROR和INCLUDE，可组合选择，一般选REQUEST。全部设置好后重新打包、部署，这样Servlet就可以自动把所有的request转换为GBK的字符集了，是不是很方便？😁但在这里加了filter后对性能方面的影响未知，大家可以讨论一下。