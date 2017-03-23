---
layout: post
title: What's new for web development in .NET 2015?
image: /img/blog/net2015.jpg
tags: [c#,code programming]
---
<p> </p>
<p>As a web developer, In this article I will just include the features that brought to web development.</p>
<h3>.NET Framework 4.6</h3>
<p><span><span>The .NET Framework is a development platform for building apps for windows Mobile, Desktop, and Cloud platform. </span>Built upon 4.5.2, .NET 4.6</span> will be a in-place replacement for .NET 4, 4.5, 4.5.1, and 4.5.2. And supports ASP.NET 5. Basically it "<em>contains new APIs, improvements to event tracing, and many bug fixes</em>". For more information see:<strong> </strong><a href="https://msdn.microsoft.com/en-us/library/w0x726c2(v=vs.110).aspx" target="_blank"><strong>.NET Framework 2015 Preview</strong></a></p>
<h3>.NET Core 5 &amp; ASP.NET 5</h3>
<p>.NET Core 5 is designed to be ready for the cloud and cross-platform deployments and provide the ability to debug the code in Linux and Mac OS X platform. ASP.NET 5 uses the <a href="http://www.mono-project.com/">Mono runtime</a> to run on Linux and Mac.</p>
<p>With the optional Cordova extension installation, VS 2015 allow developers to build Hybrid HTML/Javascript Mobile Apps which can be deployed to Android or IOS device. </p>
<p>For more information see: <a href="http://weblogs.asp.net/scottgu/introducing-asp-net-5" target="_blank"><strong>Introducing ASP.NET 5</strong></a></p>
<h3><strong>MVC 6</strong></h3>
<p>1. CSHTML New tag helpers feature.</p>
<p>previous: </p>
<pre><code>@Html.LabelFor(m =&gt; m.UserName, new { @class = "control-label" })<br /></code></pre>
<p>Now it will be like:</p>
<pre><code><span>&lt;</span><span>label</span><span> </span><span>asp-for</span><span>="UserName"</span><span> </span><span>class</span><span>="control-label"&gt;&lt;/</span><span>label</span><span>&gt;</span></code><code></code></pre>
<p>2. Built-in Dependency Injection</p>
<p><span>MVC 6 has dependency injection built in to the framework. </span>Just need to register the repository with the dependency injection system in the <strong>Startup</strong> Class </p>
<pre><code class="prettyprint prettyprinted"><span class="kwd">public </span><span class="kwd">void </span><span class="typ">ConfigureServices</span><span class="pun">(</span><span class="typ">IServiceCollection</span><span class="pln"> services</span><span class="pun">)</span><span class="pun">{<br /></span><span class="pln">    services</span><span class="pun">.</span><span class="typ">AddMvc</span><span class="pun">();<br /></span><span class="com">    // New code<br /></span><span class="pln">    services</span><span class="pun">.</span><span class="typ">AddSingleton</span><span class="pun">&lt;</span><span class="typ">IMyRepository</span><span class="pun">,My</span><span class="typ">Repository</span><span class="pun">&gt;();<br /></span></code></pre>
<h3>c# 6.0</h3>
<ul>
<li>New <strong>nameof</strong> expressions</li>
<li>String interpolation</li>
<li>Null-conditional operators</li>
<li>Index initializers </li>
<li>Extension Add methods </li>
<li>Auto-property initializers</li>
<li>Import static members of types directly into scope</li>
</ul>
<p>You can find out about the features in this link:<a href="http://blogs.msdn.com/b/csharpfaq/archive/2014/11/20/new-features-in-c-6.aspx"> New Features in c# 6</a></p>