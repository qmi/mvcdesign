---
layout: post
title: What happens if throwing an exception in a Lock statement?
image: /img/blog/lock.jpg
tags: [c#,code programming]
---
A further look into how is the lock statement working in deep? And an experiment of what will happen when throws the exception within the lock statement?

<p>Say we have a lock statement as below:</p>
<pre><code><br />lock(syncObject){   <br />   ...<br />   Throw new Exception("");<br />   ...<br />}<br /></code></pre>
<p>Will the thread on the synObject get released after throw the exception?</p>
<p>To find out the answer, we need to understand how the lock is working essentially. In MSDN, it explain the lock procedures: </p>
<pre>"Use Enter to acquire the Monitor on the object passed as the parameter. If another thread has executed an Enter on the object but has not yet executed the corresponding Exit, the current thread will block until the other thread releases the object. It is legal for the same thread to invoke Enter more than once without it blocking; however, an equal number of  Exit calls must be invoked before other threads waiting on the object will unblock."</pre>
<p> The C# <strong>lock</strong> keyword wraps the Enter and Exit methods in a<em> try…finally</em> block. In c# 4.0 lock (<a href="http://blogs.msdn.com/b/ericlippert/archive/2009/03/06/locks-and-exceptions-do-not-mix.aspx">here</a>) the code above is translate as follows:</p>
<pre><code>bool lockWasTaken = false;<br />var temp = syncObject<br /></code><code>try{<br />  Monitor.Enter(temp, ref lockWasTaken);<br />  //Custom code here<br />  Throw new Exception("");<br />  ...<br />} finally{<br />  if(lockWasTaken){<br />    Monitor.Exit(temp);<br />  }<br />}<br /><br /></code></pre>
<p>As you can see, the lock is always released in a finally statement. So even there is an exception error in the lock statement, the thread will get released eventually.</p>

