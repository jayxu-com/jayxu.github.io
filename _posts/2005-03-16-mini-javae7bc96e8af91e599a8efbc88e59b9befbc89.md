---
id: 15481
title: 'Mini Java编译器（四）'
date: '2005-03-16T11:24:02+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15481'
permalink: /2005/03/16/15481
posturl_add_url:
    - 'yes'
views:
    - '2196'
dsq_thread_id:
    - '4930736813'
duoshuo_thread_id:
    - '6.3356053327939E+18'
---

<h2>四、P代码指令说明</h2>
由于系统较简单，所以对底层硬件也做了简化：
<ol>
 	<li>没有寄存器，只有一个数据栈</li>
 	<li>只能对主存进行存、取操作</li>
 	<li>只支持主存间接寻址</li>
 	<li>可以查找符号表中符号，返回该符号地址</li>
</ol>
&nbsp;
<h3>指令表（未完成）</h3>
<table>
<tbody>
<tr>
<th>助记符</th>
<th>格式</th>
<th>说明</th>
</tr>
<tr>
<td>push</td>
<td>push &lt;address&gt;</td>
<td>将&lt;address&gt;指向的内容压栈</td>
</tr>
<tr>
<td>pop</td>
<td>pop &lt;address&gt;</td>
<td>将栈顶内容弹入&lt;address&gt;指向的位置</td>
</tr>
<tr>
<td>jmp</td>
<td>jmp &lt;address&gt;</td>
<td>无条件跳转至&lt;address&gt;指向的代码</td>
</tr>
<tr>
<td>jt</td>
<td>jt &lt;address&gt;, &lt;goal&gt;</td>
<td>如果&lt;address&gt;指向的内容为真则跳转至&lt;goal&gt;指向的代码</td>
</tr>
</tbody>
</table>
&nbsp;
<h2>五、错误信息表</h2>
（定义在compiler.exception.ErrorMessage接口中）
<table>
<tbody>
<tr>
<td>ANALYZING_FAILURE</td>
<td>文件无法分析</td>
</tr>
<tr>
<td>CLASS_DEFINED</td>
<td>重复类定义</td>
</tr>
<tr>
<td>CLASS_NOT_DEFINED</td>
<td>类未定义</td>
</tr>
<tr>
<td>IDENTIFIER_DEFINED</td>
<td>重复标识符定义</td>
</tr>
<tr>
<td>IDENTIFIER_NOT_DEFINED</td>
<td>标识符未定义</td>
</tr>
<tr>
<td>ILLEGAL_EXPRESSION</td>
<td>非法表达式</td>
</tr>
<tr>
<td>ILLEGAL_GRAMMER</td>
<td>语法错误</td>
</tr>
<tr>
<td>ILLEGAL_OPERATION</td>
<td>非法操作</td>
</tr>
<tr>
<td>ILLEGAL_TOKEN</td>
<td>标识符无法分析</td>
</tr>
<tr>
<td>METHOD_DEFINED</td>
<td>重复方法定义</td>
</tr>
<tr>
<td>NOT_ALLOCATED</td>
<td>内存未分配</td>
</tr>
<tr>
<td>OUT_OF_MEMORY</td>
<td>内存已满</td>
</tr>
<tr>
<td>READ_FILE</td>
<td>文件无法读取</td>
</tr>
<tr>
<td>TYPE_UNMATCHED</td>
<td>类型不匹配</td>
</tr>
</tbody>
</table>