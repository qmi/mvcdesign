---
layout: post
title: How to manage the ASP.NET MVC state information?
image: /img/blog/sessionmanagement.jpg
tags: [ASP.NET MVC]
---
<p>In an ASP.NET MVC 4 application, state information can be stored in different locations. They are all for different scenario usages and purposes. typical ones are as below: </p>
<h3>Cache</h3>
<p>A memory pool stored on the server and shared across users.</p>
<p>A typical one is the Http cache defined at System.Web.caching, it can be used from the  HttpRuntime.Cache,</p>
<pre> HttpRuntime.Cache.Insert(key, value)</pre>
<p>Or you can create a custom Memory Cache help to manage the cache items</p>
<pre><span>ObjectCache cache = System.Runtime.Caching.MemoryCache.Default;<br />cache["apple"] = "sweet apple";<br /><span>string apple = cache["apple"] as string;</span><br /></span></pre>
<h3>Session</h3>
<p>Stored on the server and unique for each user request. The value is persist for multiple requests, It's default to 20 minutes timeout. The time out value can be set the value at web.config:</p>
<pre>&lt;system.web&gt;
    &lt;sessionState 
      mode="InProc"
      cookieless="true"
      timeout="30" /&gt;
  &lt;/system.web&gt;</pre>
<p>Note that session can be store in different modes: InProc, <span class="input">StateServer,</span><span> <span>SQLServer, Custom, or Off which disable the session state.</span></span> </p>
<p>Find out more setting at: https://msdn.microsoft.com/en-us/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx</p>
<h3>Cookies</h3>
<p>Stored on the client and passed with each HTTP request to the server.</p>
<p>It can be set in the Response object,</p>
<p>c# to set and get cookie:</p>
<pre>//Add a cookie<br />Response.Cookies[<span>"fruit"</span>].Value = <span>"apple"</span>;<br />//Get cookie<br />var fruit = Request.Cookies[""]</pre>
<p>Javascrip to set/get cookie:</p>
<pre><span>//Add a cookie<br />document.cookie=document.cookie + ";fruit=applie"<br />//Get cookie<br />var</span><span> x = document.cookie;</span></pre>
<p>Note that cookies are usually limited vary by browsers, mostly support up to 2096 bytes, which is rather small amount of data.</p>
<h3>QueryString</h3>
<p>Passed as part of the complete URL string, like a url page:</p>
<p><em>http://exampleUrl.com/search?query=apple</em></p>
<p>To the a query string in request:</p>
<pre>var query = Request.<span style="text-decoration: underline;">QueryString</span>["query"];</pre>
<p>In asp.net mvc, it can be configured to a relative path via the routing configuration:</p>
<p><em>http://exampleUrl.com/search/apple</em></p>
<p>while the search is a controller defined as:</p>
<pre>public class Search{<br /><br />  public ActionResult Index(string query){<br />         //Your Statement<br />  }<br /><br />}</pre>
<h3>Context Items</h3>
<p>part of the HttpContext and lasts only the lifetime of that request. According to MSDN</p>
<p>https://msdn.microsoft.com/en-us/library/system.web.httpcontext.items(v=vs.110).aspx</p>
<p><em>"Gets a key/value collection that can be used to organize and share data between an <a href="https://msdn.microsoft.com/en-us/library/system.web.ihttpmodule(v=vs.110).aspx">IHttpModule</a> interface and an <a href="https://msdn.microsoft.com/en-us/library/system.web.ihttphandler(v=vs.110).aspx">IHttpHandler</a> interface during an HTTP request."</em></p>
<pre>//Set items<br />HttpContext.Current.Items["key"]= "AnApple";<br />//Get the item<br />var item = (string)HttpContext.Current.Items["key"]</pre>
<p>The collections only keep the value for a single request, when you call a Response.Redirect, the value will be lost.</p>
<h3>Profile</h3>
<p>Profile stored in database, XML or Web Service, and it maintains information across multiple sessions. This means that profile data last for a long time unless it's manipulated to be deleted.</p>
<p>It can be defined in the web.config file in the profile section:</p>
<pre>&lt;profile&gt;
  &lt;properties&gt;
    &lt;add name="FirstName" /&gt;
  &lt;/properties&gt;
&lt;/profile&gt;</pre>
<p>More about how profile works can be found at: </p>
<p>https://msdn.microsoft.com/en-us/library/d8b58y5d.aspx</p>
<p> </p>