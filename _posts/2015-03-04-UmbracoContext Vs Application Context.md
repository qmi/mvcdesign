---
layout: post
title: UmbracoContext Vs Application Context
image: /img/blog/umbracocontext.jpg
tags: [HTML5,CSS3,Javascript]
---
<p>We can get the content cache and services from both <strong>UmbracoContext.Current</strong> and <strong>ApplicationContext.Current</strong>. It leads to a question which one to use in my class?</p>
<p>A bit of research further in the Umbraco API (see the <a href="#references">references</a>) and find out that, </p>
<p><strong>UmbracoContext</strong> is under the Umbraco.Web namespace:</p>
<p><em>"Class that encapsulates Umbraco information of a specific HTTP request."</em></p>
<p><span>It also has a property named <em>Application</em> which is also a type of the Application Context.</span></p>
<p>While <strong>ApplicationContext</strong> is under the Umbraco.Core namespace:</p>
<p><em>"represents the global Umbraco application"</em></p>
<p>So we can see that they are serving in different purpose, The Umbracocontext is built on the HTTP request objects, while ApplicationContext is operated outside of web context.</p>
<p>The most frequent mistakes is people trying to get the UmbracoContext in a custom Task scheduler and find that UmbarcoContext.Current is actually null. And misuse the ApplicationContext in the Web Controller.</p>
<h3>UmbracoContext should be used in:</h3>
<ul>
<li>Controller Actions and View files</li>
<li>Custom Httpmodules and Custom httpHandlers</li>
</ul>
<h3>ApplicationContext should be used in:</h3>
<ul>
<li>Application Startup Handler</li>
<li>Task Scheduler</li>
<li>Rebuild the search index</li>
</ul>
<p> </p>
<p id="references">References:</p>
<p>https://our.umbraco.org/apidocs/csharp/api/Umbraco.Web.UmbracoContext.html</p>
<p>https://our.umbraco.org/apidocs/csharp/api/Umbraco.Core.ApplicationContext.html</p>