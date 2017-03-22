---
layout: post
title: html code and pre tag difference
image: /img/hello_world.jpeg
tags: [HTML5,CSS3,Javascript]
---

<h3><code>&lt;Pre&gt;</code> Represents a block of preformatted text</h3>
<p>In pre tag,<strong> it preserves the spaces and line breaks</strong>. It's ideally used for indented format text, ex. Email text, draft essays, computer code.</p>
<p>For example:</p>
<pre>&lt;pre&gt;<br />Hi Mr.<br />    How are you recently, ...<br /><br />Regards,<br />Name<br /><br />&lt;/pre&gt;</pre>
<p>which output like this:</p>
<pre>Hi Mr.<br />    How are you recently, ...<br /><br />Regards,<br />Name</pre>
<p> </p>
<h3><code>&lt;Code&gt; </code> Designates a fragment of computer code</h3>
<p><span>Designates a fragment of computer code. <span>could be something like an XML format code, program code, "<em>or any other string that a computer would recognize"</em>.</span></span></p>
<p>It can be also added a class prefixed with "<code title="">language-</code>" to the element.</p>
<p>For example:</p>
<pre>&lt;code class="language-html"&gt;<br />   &lt;div&gt;<br />         ...<br />   &lt;div&gt;<br />&lt;/code&gt;</pre>
<p>The purpose of mark the class is to let the syntax highlighting scripts determine the right rules.</p>
<p><code> &lt;pre&gt;&lt;code&gt;</code> is combined to used in many cases to display a block of the programming codes. so the coding format is keep indented.</p>
<p>For example:</p>
<pre>&lt;pre&gt;<br />  &lt;code class="language-html"&gt;<br />   &lt;div&gt;<br />         ...<br />   &lt;div&gt;<br />  &lt;/code&gt;<br />&lt;/pre&gt;</pre>
<p>which output like this:</p>
<pre>   &lt;div&gt;<br />         ...<br />   &lt;div&gt;</pre>
<p> </p>