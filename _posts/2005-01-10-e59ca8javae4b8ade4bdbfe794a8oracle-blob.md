---
id: 15424
title: '在Java中使用Oracle blob'
date: '2005-01-10T14:04:46+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15424'
permalink: /2005/01/10/15424
posturl_add_url:
    - 'yes'
views:
    - '1800'
dsq_thread_id:
    - '4929077804'
duoshuo_thread_id:
    - '6.3356053013408E+18'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<!-- wp:paragraph -->
<p>Oracle中的lob (Large Object)可以存储非常大的数据（可能是4GB），这样就可以通过将文件或其它任何对象序列化成字节输出流(OutputStream)后写入数据库，之后使用字节输入流(InputStream)将数据读出然后反序列化为原始文件或对象。操作时需要使用oracle的JDBC包，它扩展了sun的JDBC包中的Blob对象。同时需要注意一些细节。下面的代码演示如何使用blob（实例中需要Oracle的JDBC包）。</p>
<!-- /wp:paragraph -->

<!-- wp:enlighter/codeblock -->
<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">import oracle.jdbc.OracleResultSet; // 使用Oracle的ResultSet对象
import oracle.sql.BLOB; // 使用Oracle的BLOB对象，而不是sun的Blob

...

try{
  Connection conn = &lt;数据库连接>;
  File file = &lt;存入数据库的文件对象>;
  conn.setAutoCommit(false); // 取消Connection对象的auto commit属性
  String file_name = file.getName();

  // 数据库中有一个item表，其中的file_name (varchar2)存储文件名，file_blob (blob)存储文件对象
  String sql = "INSERT INTO item (file_name,file_blob) VALUES ('" + file_name + "',EMPTY_BLOB())"; // 使用“EMPTY_BLOB()“成生一个空blob
  Statement stmt = conn.createStatement();
  int count = stmt.executeUpdate(sql);
  
  sql = "SELECT file_blob FROM item WHERE iid='" + iid + "' FOR UPDATE"; // 使用“FOR UPDATE”得到表的写锁
  ResultSet rs = stmt.executeQuery(sql);
  rs.next();

  BLOB blob = ((OracleResultSet)rs).getBLOB("file_blob"); // 得到BLOB对象
  OutputStream out = blob.getBinaryOutputStream(); // 建立输出流
  InputStream in = new FileInputStream(file); // 建立输入流
  int size = blob.getBufferSize();
  byte[] buffer = new byte[size]; // 建立缓冲区

  int len;
  while((len = in.read(buffer)) != -1)
    out.write(buffer,0,len);

  in.close();
  out.close();

  conn.commit();
} catch(Exception ex) {
  try {
    conn.rollback();
  } catch(SQLException sqle) {
    System.err.println(sqle.getMessage());
  }
}
</pre>
<!-- /wp:enlighter/codeblock -->

<!-- wp:paragraph -->
<p>如果要读出文件的话只需调用BLOB的getBinaryStream()生成一个输入流，再写入一个文件就行了。</p>
<!-- /wp:paragraph -->