---
layout: post
title: Different ways to to truncate string with ellipsis
image: /img/blog/vs2013.jpg
tags: [asp.net MVC]
---
Some times we need to display the summary text being replaced with ellipsis characters, while the text has exceed a specified length. There are a few approaches to achieve this.
#### Method 1 in Code Behind c#:
<p>Program it in in the code behind. Such as below c# string extension:</p>
<pre><code>public static string ToEllipsis(this string oldStr, int maxLength, string replaceChars = "...")<br />{<br />  var newStr = oldStr;<br />  if (oldStr.Length &lt; maxLength)<br />  {<br />   return oldStr;<br />  }<br />  var newstring = newStr.Substring(0, maxLength);<br />  newstring = newstring.TrimEnd();  //In case there are some space.<br />  newstring += replaceChars;<br />  return newstring;<br />}</code></pre>
<p>run the code in Main it will look like:</p>
<pre><code>var testStr = "I way to say thank you to readding this blog";</code><code>  <br />Console.WriteLine(testStr.ToEllipsis(10));<br />//output: I want to s...<br /><br />Console.WriteLine(testStr.ToEllipsis(10,"---")<br />//output: I want to s---<br /><br /></code></pre>
<p>As you see, in this method, you could also pass in other characters as well besides "...".</p>
<p><strong>Method 2 using CSS:</strong></p>
<p>There is another simple way to just truncate the string using <em>text-overflow:ellipsis</em> in css3.</p>
<pre><code>.truncate {<br /> width: 100px;<br /> white-space: nowrap;<br /> overflow: hidden;<br /> text-overflow: ellipsis;<br />}</code></pre>
<p>Result:</p>
<pre><code>&lt;p class="truncate"&gt;This is a paragraph.&lt;/p&gt;<br /></code><code>//output: <span>This is a par...</span></code></pre>
<p> There are some drawbacks with this method, that it doesn't limit the string by the character length, but by the box length. </p>
<p> To resolve this, we can use the<em> ch</em> unit instead of <em>px</em> unit to limit the character number. Be aware that ch is is only supported by the latest version browsers.</p>
<p> See below: </p>
<pre><code>.truncate {<br /><strong> width: 10ch;</strong><br /> white-space: nowrap;<br /> overflow: hidden;<br /> text-overflow: ellipsis;<br />}</code></pre>
<p>Result:</p>  
<pre>	&lt;p class="truncate"&gt;This is a paragraph.&lt;/p&gt;
	//output: This is a 		...
</pre>
<p>Note that If it happens to be a space character in the specific length, the text will not get trimmed.</p>
<h3>Method 3 Using Angular</h3>
<p>There is a much simple solution if you are using angular with the filter feature:</p>
<pre>	{{ myText| limitTo : 50 }}{{ myText.length &gt; 50 ? '...' : '' }}</pre>

 
 