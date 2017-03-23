---
layout: post
title: Web API Controller asynchronous issue with email client
image: /img/blog/emailclient.jpg
tags: [c#,code programming]
---
<h3>The Problem:</h3>
<p>Recently when I was trying to using the email client to send an email via the Web Api controller, I came across an exception message below:</p>
<p><code> <span>An asynchronous module or handler completed while an asynchronous operation was still pending.</span></code></p>
<p>I was using the code as below using an email client to send out the message asynchronously:</p>
<pre><code>public void SendEmail(){<br /> using (var client = new SmtpClient())</code><code> <br />        {<br /></code><code>           var msg = new MailMessage(&lt;from&gt;, &lt;to&gt;);<br /></code><code>           msg.Subject = "some";<br /></code><code>           msg.Body = "abc";</code><code><br />           client.SendAsync(msg, null);</code><code>     <br />          }<br />}</code></pre>
<h3>Cause:</h3>
<p>According to https://msdn.microsoft.com/en-us/library/x5x13z6h(v=vs.110).aspx.</p>
<p>The SendAsync is developed since .NET2.0 and can't use the await. When the client call the SendAsync method, it registers the asynchronous operation with the ASP.NET <em>SynchronizationContext</em>. So when the controller returns, and it sees that a pending asynchronous operations has not yet complete, and then raise the exception. </p>
<h3>The Solution:</h3>
<p>The simple solution for that is using the async task to wrap the method :</p>
<pre><code>Task.Run(async () =&gt;<br />   { <br />     SendEmail();</code><code><br />   }</code></pre>
<p>This is works fine after I deployed to our live environment. However it might still have an issue for a rare scenario which I will ignore for now before I find another solution. That when the app pool is recycling, the background tasks will be abnormally aborted and result into that the send email fail to proceed. </p>
<p>Alternatively might be able to use the <strong>SendMailAsync</strong> Method. Not sure if it will resolve the issue, I haven't gotten the chance to test this out yet.</p>
<p> </p>
<p>Reference:</p>
<p>https://msdn.microsoft.com/en-us/library/system.net.mail.smtpclient_methods(v=vs.110).aspx</p>
<p> </p>
