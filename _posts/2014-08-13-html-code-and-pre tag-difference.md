---
layout: post
title: html code and pre tag difference
image: /img/blog/html5.png
tags: [HTML5,CSS3,Javascript]
---
As I trying to writing this blog, I come across my first question: should I use code or pre? what
is the difference?


<code>&lt;Pre&gt;</code> Represents a block of preformatted text
In pre tag,<strong> it preserves the spaces and line breaks</strong>. It's ideally used for indented format text, ex. Email text, draft essays, computer code.
For example:
<pre>&lt;pre&gt;<br />Hi Mr.<br />    How are you recently, ...<br /><br />Regards,<br />Name<br /><br />&lt;/pre&gt;</pre>
which output like this:
<pre>Hi Mr.<br />    How are you recently, ...<br /><br />Regards,<br />Name</pre>

<code>&lt;Code&gt; </code> Designates a fragment of computer code
Designates a fragment of computer code. could be something like an XML format code, program code, "<em>or any other string that a computer would recognize"</em>.
It can be also added a class prefixed with "<code title="">language-</code>" to the element.
For example:
<pre>&lt;code class="language-html"&gt;<br />   &lt;div&gt;<br />         ...<br />   &lt;div&gt;<br />&lt;/code&gt;</pre>
<p>The purpose of mark the class is to let the syntax highlighting scripts determine the right rules.</p>
<p><code> &lt;pre&gt;&lt;code&gt;</code> is combined to used in many cases to display a block of the programming codes. so the coding format is keep indented.</p>
<p>For example:</p>
	<pre>
	  <code class="language-html">
	   <div>
			 ...
	   <div>
	  </code>
	</pre>
<p>which output like this:</p>
	<div>
         ...
	<div>
