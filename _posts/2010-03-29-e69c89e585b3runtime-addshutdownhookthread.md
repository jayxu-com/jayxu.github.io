---
id: 2101
title: 有关Runtime.addShutdownHook(Thread)
date: '2010-03-29T20:38:31+08:00'
author: Jay
layout: post
guid: 'http://jayxu.com/2010/03/29/2101/'
permalink: /2010/03/29/2101
aktt_notify_twitter:
    - 'yes'
    - 'yes'
aktt_tweeted:
    - '1'
    - '1'
views:
    - '4484'
shorturl:
    - 'http://goo.gl/J5QQI'
posturl_add_url:
    - 'yes'
duoshuo_thread_id:
    - '6.335604581766E+18'
dsq_thread_id:
    - '4357086018'
---

<p>今天在JDK的javadoc里瞎转的时候无意间发现这么一个有趣的回调方法：</p>
<blockquote>
<h3> addShutdownHook</h3>
<pre>public void <b>addShutdownHook</b>(<a href="http://download.oracle.com/javase/6/docs/api/java/lang/Thread.html" title="class in java.lang">Thread</a> hook)</pre>
<dl>
<dd>
<p>Registers a new virtual-machine shutdown hook.</p>
<p> The Java virtual machine <i>shuts down</i> in response to two kinds of events:    </p>
<ul>
<li> The program <i>exits</i> normally, when the last  non-daemon   thread exits or when the <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/Runtime.html"><pre class="inline:true decode:1 " >exit</pre></a></tt> (equivalently,   <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/System.html"><pre class="inline:true decode:1 " >System.exit</pre></a></tt>) method is invoked, or

</li>
<li> The virtual machine is <i>terminated</i> in  response to a   user interrupt, such as typing <tt>^C</tt>, or a system-wide event,   such as user logoff or system shutdown.    </li>
</ul>
<p> A <i>shutdown hook</i> is simply an initialized but unstarted thread.  When the virtual machine begins its shutdown sequence it will start all registered shutdown hooks in some unspecified order and let them run concurrently.  When all the hooks have finished it will then run all uninvoked finalizers if finalization-on-exit has been enabled. Finally, the virtual machine will halt.  Note that daemon threads will continue to run during the shutdown sequence, as will non-daemon  threads if shutdown was initiated by invoking the <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/Runtime.html"><pre class="inline:true decode:1 " >exit</pre></a></tt> method.  </p>
<p> Once the shutdown sequence has begun it can be stopped only by invoking the <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/Runtime.html"><pre class="inline:true decode:1 " >halt</pre></a></tt> method, which forcibly terminates the virtual machine.  </p>
<p> Once the shutdown sequence has begun it is impossible to  register a new shutdown hook or de-register a previously-registered hook. Attempting either of these operations will cause an <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/IllegalStateException.html" title="class in java.lang"><pre class="inline:true decode:1 " >IllegalStateException</pre></a></tt>  to be thrown.  </p>
<p> Shutdown hooks run at a delicate time in the life cycle of a  virtual machine and should therefore be coded defensively.  They should, in particular, be written to be thread-safe and to avoid deadlocks insofar as possible.  They should also not rely blindly upon services that may have registered their own shutdown hooks and therefore may themselves  in the process of shutting down.  Attempts to use other thread-based services such as the AWT event-dispatch thread, for example, may lead  to deadlocks.  </p>
<p> Shutdown hooks should also finish their work quickly.  When a program invokes <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/Runtime.html"><pre class="inline:true decode:1 " >exit</pre></a></tt> the expectation is that the virtual machine will promptly shut down and exit.  When the virtual machine is terminated due to user logoff or system shutdown the underlying operating system may only allow a fixed amount of time in which to shut down and exit.  It is therefore inadvisable to attempt  any user interaction or to perform a long-running computation in a shutdown hook.  </p>
<p> Uncaught exceptions are handled in shutdown hooks just as in  any other thread, by invoking the <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/ThreadGroup.html"><pre class="inline:true decode:1 " >uncaughtException</pre></a></tt> method of the thread's <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/ThreadGroup.html" title="class in java.lang"><pre class="inline:true decode:1 " >ThreadGroup</pre></a></tt> object.   The default implementation of this method prints the exception's stack trace to <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/System.html"><pre class="inline:true decode:1 " >System.err</pre></a></tt> and terminates the thread; it does not cause the virtual machine to exit or halt.  </p>
<p> In rare circumstances the virtual machine may <i>abort</i>,  that is, stop running without shutting down cleanly.  This occurs when the virtual machine is terminated externally, for example with the <tt>SIGKILL</tt> signal on Unix or the <tt>TerminateProcess</tt> call  on Microsoft Windows.  The virtual machine may also abort if a native method goes awry by, for example, corrupting internal data structures  or attempting to access nonexistent memory.  If the virtual machine aborts then no guarantee can be made about whether or not any shutdown hooks will be run. </p>

</dd>
<dd>
<dl>
<dt><b>Parameters:</b></dt>
<dd><pre class="inline:true decode:1 " >hook</pre> - An initialized but  unstarted <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/Thread.html" title="class in java.lang"><pre class="inline:true decode:1 " >Thread</pre></a></tt> object </dd>
<dt><b>Throws:</b> </dt>
<dd><pre class="inline:true decode:1 " ><a href="http://java.sun.com/javase/6/docs/api/java/lang/IllegalArgumentException.html" title="class in java.lang">IllegalArgumentException</a></pre> - If the specified hook has already been registered,          or if it can be determined that the hook is already running or          has already been run </dd>
<dd><pre class="inline:true decode:1 " ><a href="http://download.oracle.com/javase/6/docs/api/java/lang/IllegalStateException.html" title="class in java.lang">IllegalStateException</a></pre> - If the  virtual machine is already in the process          of shutting down </dd>
<dd><pre class="inline:true decode:1 " ><a href="http://java.sun.com/javase/6/docs/api/java/lang/SecurityException.html" title="class in java.lang">SecurityException</a></pre> - If a security manager is present and it denies          <tt><a href="http://download.oracle.com/javase/6/docs/api/java/lang/RuntimePermission.html" title="class in java.lang"><pre class="inline:true decode:1 " >RuntimePermission</pre></a>("shutdownHooks")</tt></dd>
<dt><b>Since:</b></dt>
<dd>1.3</dd>
<dt><b>See Also:</b></dt>
<dd><a href="http://download.oracle.com/javase/6/docs/api/java/lang/Runtime.html"><pre class="inline:true decode:1 " >removeShutdownHook(java.lang.Thread)</pre></a>,  <a href="http://download.oracle.com/javase/6/docs/api/java/lang/Runtime.html"><pre class="inline:true decode:1 " >halt(int)</pre></a>,  <a href="http://download.oracle.com/javase/6/docs/api/java/lang/Runtime.html"><pre class="inline:true decode:1 " >exit(int)</pre></a></dd>
</dl>
</dd>
</dl>
</blockquote>
<p>即可以在runtime对象上注册一个回调方法，该方法会在JVM退出时执行传入的线程对象。在mac下试了一下，当调用System.exit()、使用系统kill命令杀掉java进程时该方法都会被调用。但是需要注意的是，当调用kill -9杀进程时，方法不被调用，JVM直接退出，Ｗindows下还没试过，不知道结果如何</p>