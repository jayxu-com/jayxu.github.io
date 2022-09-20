---
id: 1809
title: '10 things all JAVA developers should know [zz]'
date: '2009-11-11T12:06:08+08:00'
author: Jay
layout: post
guid: 'http://ijay.net.cn/2009/11/11/1809/'
permalink: /2009/11/11/1809
aktt_notify_twitter:
    - 'no'
    - 'no'
views:
    - '7664'
shorturl:
    - 'http://goo.gl/U00fb'
duoshuo_thread_id:
    - '6.3356044687043E+18'
---

原文在<a href="http://armelnene.blogspot.com/2009/11/10-things-all-java-developers-should.html" target="_blank">这里</a>

Since JAVA (I know it's not an acronym, but it stands out like that) was officially introduced in 1995, it has changed the way most of us look at the Operating System. Bill Gate (how ironic) once said that it was not about the hardware but the software which will be the future. A decade or more later, the fifth employee of SUN, John Gage said "The Network is the Computer". Fast-forwarding to the 21st century and John seemed to be right. Anyway, JAVA was built not to depend on an Operating System and deployed through the network. JAVA through its applet technology gave birth to Rich Network Application aka Rich Internet Application (RIA). JAVA is not perfect; or we would not have various releases and more on the way, but JAVA has given birth to a wide range of programming language (just Google it to find out more). Without further ado, I am going to get back to subject. This is a brief
article on what I believe that every Java developers should know regardless of their experience. I do not personally believe that someone with 5 years experience is not as good as someone with 10 years experience. We all develop our own methods of working but as a developer you need to stay abreast of your technology. So, here are my top 10 not in order of importance (or?):
<ol>
	<li><strong>Remember the basic of JAVA language and OOP paradigm.</strong>Most experience developers seem to forget the theory behind the language. I am not saying that they are not good at their job but can they explain to junior developers why they have used interfaces instead of abstract classes or why implement a pattern over another one? As a programmer, you become very arrogant as you believe that you write the best code but in the real world, people work in teams with different skill set and experiences. It is important that you can backup your actions/ codes. A very simple question such as; when should I use a String object instead of a StringBuilder/ StringBuffer? You might take this question lightly but can you actually tell someone else the
difference?</li>
	<li><strong>Know your technology stack</strong>All developers have to know their technology stack. What does it mean? JAVA is not like other languages; JAVA has subsets such J2ME and superset such as Java EE. We have our own area of expertise but it is important to know the differences between the various sets of JAVA. Some basic questions such as the differences between SWING, Applet,
Servlets, EJBs and JAVAFX will boost your confidence. Most developers do not know how to tweak the JVM and the differences between the JRE and the SDK environment. Do you know why you need the SDK to be installed to run Tomcat but you only need the JRE to run an application?</li>
	<li><strong>Experiment with various Java EE framework</strong>I am not asking you to be an expert in every single Java EE framework but it will make the difference if you are familiar with Spring and EJB. That should actually be the de facto framework that should be on every developers CV. Developers should know the difference between Java EE 5 (soon 6) and Spring. Hibernate is also brilliant and it's used for data access but all developers should have moved to JPA by now. Hibernate also comply with JPA therefore there is no more excuses.</li>
	<li><strong>Know a scripting language</strong>JAVA can be heavyweight for some simple tasks which can be implemented using a simple dynamic language such as Python, Perl(?) and others. I would also recommend to developers to learn shell scripting on their target OS.</li>
	<li><strong>Know how to develop web services</strong>The network is the computer, therefore it is important to know the different web services framework available. Data are integrated through web services and opening your services to the "cloud". SWING developers will probably not develop web services but I am sure that they will be connecting to data through web services clients. Understanding the difference between the standardised SOAP and non-standardised ReST will help you choose which is best to implement your services.</li>
	<li><strong>Know how and when to multithread your application</strong>I have to put that in there. Developers should know when and why to multithread an application, thread inter-communication and monitoring. All developers, junior or not, should know how to write a multi-threaded application.</li>
	<li><strong>Database development using JDBC and JPA</strong>This should be a development law. All developers should know how to write SQL queries and how to create databases. All enterprise applications store data in some sort of relational database systems and it is therefore imperative that this knowledge should be of second nature. Java EE 5 introduced JPA (JDO was there before) but it is not
applicable to all situation. Hence, knowing the difference and when to implement one instead of the other is important.</li>
	<li><strong>Know a client side scripting language and what is AJAX</strong>The network is the computer and Internet is the deployment platform. Java EE and its various framework are server side executiong which can put extra "load" on the server. If you are looking to move a cloud based system where the providers charges you per resources used, it might be wise to move some of the execution to the client side. AJAX
has been buzzing the scene for the last 3 years and more. This is not a technology but a new way of doing something that already existed. There are numerous JAVA AJAX framework such as GWT and DWR which makes it easy to develop AJAX based application which are compiled to JavaScript. Developers should also know what is the AJAX theories.</li>
	<li><strong>Know your competitors and do not take part on "what is the best IDE" discussion</strong>JAVA is not the only language that can do what it does. I think that JAVA is more mature and complete as opposed to other languages. Knowing the difference between JAVA and .NET or JAVA and Ruby is a good asset to have. You also need to know when and why to use one instead of the other. Please please please, do not get into "my IDE is better than x because..." discussion as it is good for the JAVA community to have multiple IDEs and framework available to use. Every tools have their place as for example JDeveloper is better than x if you are going to solely develop on an Oracle stack and etc...</li>
	<li><strong>Know ANT (MAVEN?), TOMCAT and any other mainstrean application server</strong>ANT is the de facto build script for JAVA and its IDE-based development. Maven is becoming popular and soon can be as popular as ANT (not sure of its popularity in the financial sector). TOMCAT should be immortalised as the based servlet container that all developers should be familiar with.</li>
</ol>
There are alot more to add but this is just some of the basics that I think all developers should have in their repertoire. Feel free to add to this list in the comments box. If I could had another one to this, would be; all developers not just JAVA, should know how to search the web and Google is your best friends (<strong>now support my advertisers by clicking on the links on the right ;)</strong> ). I hope you enjoyed the entry and feel free to comments good or bad!!! are welcome.