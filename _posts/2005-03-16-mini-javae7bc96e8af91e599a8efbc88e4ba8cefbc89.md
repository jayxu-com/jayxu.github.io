---
id: 15469
title: 'Mini Java编译器（二）'
date: '2005-03-16T11:13:33+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15469'
permalink: /2005/03/16/15469
posturl_add_url:
    - 'yes'
views:
    - '2143'
dsq_thread_id:
    - '4929518882'
duoshuo_thread_id:
    - '6.3356053326303E+18'
---

<h2>二、Mini Java的文法</h2>
<h3>BNF</h3>
<table>
<tbody>
<tr>
<td>Goal</td>
<td>::=</td>
<td>MainClass ( TypeDeclaration )* &lt;EOF&gt;</td>
</tr>
<tr>
<td>MainClass</td>
<td>::=</td>
<td>"class" Identifier "{" "public" "static" "void" "main" "(" "String" "[" "]" Identifier ")" "{" PrintStatement "}" "}"</td>
</tr>
<tr>
<td>TypeDeclaration</td>
<td>::=</td>
<td>ClassDeclaration</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>ClassExtendsDeclaration</td>
</tr>
<tr>
<td>ClassDeclaration</td>
<td>::=</td>
<td>"class" Identifier "{" ( VarDeclaration )* ( MethodDeclaration )* "}"</td>
</tr>
<tr>
<td>ClassExtendsDeclaration</td>
<td>::=</td>
<td>"class" Identifier "extends" Identifier "{" ( VarDeclaration )* ( MethodDeclaration )* "}"</td>
</tr>
<tr>
<td>VarDeclaration</td>
<td>::=</td>
<td>Type Identifier ";"</td>
</tr>
<tr>
<td>MethodDeclaration</td>
<td>::=</td>
<td>"public" Type Identifier "(" ( FormalParameterList )? ")" "{" ( VarDeclaration )* ( Statement )* "return" Expression ";" "}"</td>
</tr>
<tr>
<td>FormalParameterList</td>
<td>::=</td>
<td>FormalParameter ( FormalParameterRest )*</td>
</tr>
<tr>
<td>FormalParameter</td>
<td>::=</td>
<td>Type Identifier</td>
</tr>
<tr>
<td>FormalParameterRest</td>
<td>::=</td>
<td>"," FormalParameter</td>
</tr>
<tr>
<td>Type</td>
<td>::=</td>
<td>ArrayType</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>BooleanType</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>IntegerType</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>Identifier</td>
</tr>
<tr>
<td>ArrayType</td>
<td>::=</td>
<td>"int" "[" "]"</td>
</tr>
<tr>
<td>BooleanType</td>
<td>::=</td>
<td>"boolean"</td>
</tr>
<tr>
<td>IntegerType</td>
<td>::=</td>
<td>"int"</td>
</tr>
<tr>
<td>Statement</td>
<td>::=</td>
<td>Block</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>AssignmentStatement</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>ArrayAssignmentStatement</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>IfStatement</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>WhileStatement</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>PrintStatement</td>
</tr>
<tr>
<td>Block</td>
<td>::=</td>
<td>"{" ( Statement )* "}"</td>
</tr>
<tr>
<td>AssignmentStatement</td>
<td>::=</td>
<td>Identifier "=" Expression ";"</td>
</tr>
<tr>
<td>ArrayAssignmentStatement</td>
<td>::=</td>
<td>Identifier "[" Expression "]" "=" Expression ";"</td>
</tr>
<tr>
<td>IfStatement</td>
<td>::=</td>
<td>"if" "(" Expression ")" Statement "else" Statement</td>
</tr>
<tr>
<td>WhileStatement</td>
<td>::=</td>
<td>"while" "(" Expression ")" Statement</td>
</tr>
<tr>
<td>PrintStatement</td>
<td>::=</td>
<td>"System.out.println" "(" Expression ")" ";"</td>
</tr>
<tr>
<td>Expression</td>
<td>::=</td>
<td>AndExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>CompareExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>PlusExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>MinusExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>TimesExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>ArrayLookup</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>ArrayLength</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>MessageSend</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>PrimaryExpression</td>
</tr>
<tr>
<td>AndExpression</td>
<td>::=</td>
<td>PrimaryExpression "&amp;&amp;" PrimaryExpression</td>
</tr>
<tr>
<td>CompareExpression</td>
<td>::=</td>
<td>PrimaryExpression "&lt;" PrimaryExpression</td>
</tr>
<tr>
<td>PlusExpression</td>
<td>::=</td>
<td>PrimaryExpression "+" PrimaryExpression</td>
</tr>
<tr>
<td>MinusExpression</td>
<td>::=</td>
<td>PrimaryExpression "-" PrimaryExpression</td>
</tr>
<tr>
<td>TimesExpression</td>
<td>::=</td>
<td>PrimaryExpression "*" PrimaryExpression</td>
</tr>
<tr>
<td>ArrayLookup</td>
<td>::=</td>
<td>PrimaryExpression "[" PrimaryExpression "]"</td>
</tr>
<tr>
<td>ArrayLength</td>
<td>::=</td>
<td>PrimaryExpression "." "length"</td>
</tr>
<tr>
<td>MessageSend</td>
<td>::=</td>
<td>PrimaryExpression "." Identifier "(" ( ExpressionList )? ")"</td>
</tr>
<tr>
<td>ExpressionList</td>
<td>::=</td>
<td>Expression ( ExpressionRest )*</td>
</tr>
<tr>
<td>ExpressionRest</td>
<td>::=</td>
<td>"," Expression</td>
</tr>
<tr>
<td>PrimaryExpression</td>
<td>::=</td>
<td>IntegerLiteral</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>TrueLiteral</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>FalseLiteral</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>Identifier</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>ThisExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>ArrayAllocationExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>AllocationExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>NotExpression</td>
</tr>
<tr>
<td></td>
<td>|</td>
<td>BracketExpression</td>
</tr>
<tr>
<td>IntegerLiteral</td>
<td>::=</td>
<td>&lt;INTEGER_LITERAL&gt;</td>
</tr>
<tr>
<td>TrueLiteral</td>
<td>::=</td>
<td>"true"</td>
</tr>
<tr>
<td>FalseLiteral</td>
<td>::=</td>
<td>"false"</td>
</tr>
<tr>
<td>Identifier</td>
<td>::=</td>
<td>&lt;IDENTIFIER&gt;</td>
</tr>
<tr>
<td>ThisExpression</td>
<td>::=</td>
<td>"this"</td>
</tr>
<tr>
<td>ArrayAllocationExpression</td>
<td>::=</td>
<td>"new" "int" "[" Expression "]"</td>
</tr>
<tr>
<td>AllocationExpression</td>
<td>::=</td>
<td>"new" Identifier "(" ")"</td>
</tr>
<tr>
<td>NotExpression</td>
<td>::=</td>
<td>"!" Expression</td>
</tr>
<tr>
<td>BracketExpression</td>
<td>::=</td>
<td>"(" Expression ")"</td>
</tr>
</tbody>
</table>