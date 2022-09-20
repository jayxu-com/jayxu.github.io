---
id: 16001
title: 'Tomcat 5.5.9 不支持switch(<enum>)？'
date: '2005-09-19T18:51:20+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=16001'
permalink: /2005/09/19/16001
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '1953'
dsq_thread_id:
    - '5287632474'
---

ServiceExceptionType：
<pre lang="java">
package pqp.service;

public enum ServiceExceptionType{
  DB_FAILURE
    ,USER_EXISTED
    ,INVALID_USERNAME_OR_PASSWORD
}</pre>

在新用户注册的逻辑方法中会检查用户名是否已存在，存在的话抛出ServiceException，并将ServiceExceptionType封装进去。action的excute不处理ServiceException，接着往外扔，最后由error.jsp处理：
<pre lang="jsp">
<%@ page contentType="text/html; charset=GBK" %>
<%@ page isErrorPage="true" %>
<%@ page import="pqp.service.*" %>

<%
ServiceException ex=(ServiceException)exception;
switch(ex.getType()){
  case USER_EXISTED:
    out.println("无法注册：用户名“"+ex.getMessage()+"”已存在");
    break;
}
%></pre>


结果编译的时候报错：

<a href="http://www.jayxu.com/log/wp-content/uploads/2016/11/tomcat.png"><img src="http://www.jayxu.com/log/wp-content/uploads/2016/11/tomcat-640x513.png" alt="" width="640" height="513" class="alignnone size-medium wp-image-16002" /></a>
难道Tomcat 5.5.9不支持对enumeration进行switch操作？