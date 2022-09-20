---
id: 12947
title: 'How do I connect my android phone to the IBM Wireless network?'
date: '2011-10-28T14:41:13+08:00'
author: Jay
layout: post
guid: 'http://www.jayxu.com/?p=12947'
permalink: /2011/10/28/12947
views:
    - '5182'
shorturl:
    - 'http://goo.gl/GOGtV'
duoshuo_thread_id:
    - '6.3356048795155E+18'
dsq_thread_id:
    - '4444662446'
---

First, if you do not have a LEAP account, you can request one in the <a href="https://bluewireless.ibm.com/">IBM Wireless Account Manager</a>
<ol>
	<li>Enter the <strong>settings application</strong>. At least for the Nexus One, I press the <strong>menu hard key </strong>then click <strong>settings</strong>.</li>
	<li>Click <strong>Wireless & networks</strong> (first option in 2.1)</li>
	<li>Click <strong>Wi-Fi settings</strong></li>
	<li>Click <strong>Add Wi-Fi network</strong></li>
	<li>Enter <strong>IBM</strong> as the <strong>Network SSID</strong>. I believe it should be all caps.</li>
	<li>Select <strong>802.1x Enterprise </strong>from the <strong>Security</strong> drop down. If you are prompted for credential store password and have never created one, set one now, I believe it has to be 6 characters long.</li>
	<li>Select <strong>PEAP</strong> from the <strong>EAP method</strong> drop down.</li>
	<li>If you see <strong>phase 2 authentication</strong> select <strong>None</strong> or <strong>N/A</strong> (also try <strong>GTC</strong> if you don't have a none option)</li>
	<li>Enter your<strong> IBM email address </strong>in <strong>Identity</strong></li>
	<li>Leave <strong>anonymous identity</strong> blank (or select <strong>None</strong>).</li>
	<li>Enter your <strong>LEAP password</strong> (not your intranet password!) in the <strong>wireless password</strong> box.</li>
</ol>
These steps have been tested with the following android versions.
<ul>
	<li>2.1-update1</li>
	<li>2.2.1</li>
	<li>2.3.4</li>
	<li>2.3.5</li>
	<li>Honeycomb 3.2</li>
</ul>
People have reported issues with the following devices.
<ul>
	<li>Samsung Galaxy SII</li>
</ul>
If the above is not working you may need to install <a href="https://market.android.com/details?id=com.oneguyinabasement.leapwifi&feature=search_result">LEAP Wifi Free</a>