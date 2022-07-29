---
id: 11592
title: 'About &#8220;IBM Rational XML ODBC Driver could not be loaded due to system error 126&#8221; when Integrating ClearQuest with Insight'
date: '2011-08-05T11:42:29+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=11592'
permalink: /2011/08/05/11592
aktt_notify_twitter:
    - 'yes'
views:
    - '6342'
aktt_tweeted:
    - '1'
shorturl:
    - 'http://goo.gl/QnQS0'
duoshuo_thread_id:
    - '6.3356048551004E+18'
dsq_thread_id:
    - '4303633171'
posturl_add_url:
    - 'yes'
---

<p>When configuring system DSN, you encounter one of the following errors: The setup routines for the IBM Rational XML ODBC Driver could not be loaded due to system error 126</p>
<p>The following steps could help you to solve:</p>
Verify the settings in the Windows registry:
<ul><li>Click <strong>Start</strong>, click <strong>Run</strong>, type regedit and click <strong>OK</strong>.</li>
<li>In the registry, go to <pre class="inline:true decode:1 " >My Computer\HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI\IBM Rational XML ODBC Driver</pre> and make sure the <pre class="inline:true decode:1 " >Driver and Setup</pre> properties point to the correct file path of ratlxml.dll.</li>
<li>In the registry, go to <pre class="inline:true decode:1 " >My Computer\HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI\ODBC Drivers</pre> and make sure <pre class="inline:true decode:1 " >IBM Rational XML ODBC Driver</pre> is found to be installed.</li>
<li>In the registry, go to <pre class="inline:true decode:1 " >My Computer\HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources</pre> and make sure the system DSN you are configuring is using <pre class="inline:true decode:1 " >IBM Rational XML ODBC Driver</pre>.</li></ul>
Verify the setting of the JDBC driver path:
<ul><li>On the desktop, right-click <strong>My Computer</strong> and click <strong>Properties</strong>,</li>
<li>On the <strong>System Properties</strong> page, click <strong>Advanced</strong> and click <strong>Environment Variables</strong>.</li>
<li>Make sure that <pre class="inline:true decode:1 " >$INSTALLDIR\jdk\jre\bin\classic</pre> is present at the beginning of the <pre class="inline:true decode:1 " >PATH</pre> or <pre class="inline:true decode:1 " >Path</pre> variables of user variables and system variables.</li></ul>
