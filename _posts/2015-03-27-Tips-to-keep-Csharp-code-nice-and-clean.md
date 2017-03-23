---
layout: post
title: Tips to to keep C# code nice and clean
image: /img/blog/c.jpg
tags: [c#,asp.net]
---
<p>Clean code that follows the good practice can help the productive of the development because the team can read the code easier, understand faster, and reduce the refactor effort on the source code in later phases.</p>
<h3>1. Keep methods short </h3>
<p>It's easier to maintain, reuse and understand if we keep the methods as short as a unit of logic. A typical bad habit is that add a new line at the end as a conditional statement when there is a bug, or a small new feature changes, which can met the requirements in a quick way. cumulatively, it leads to unreadable and unmanageable due to various changes from different stages.</p>
<p>Another drawback is, placing a long statements in one method makes it hard to resolve the source control conflicts for coordination work.</p>
<p>According to the <a href="http://csharpguidelines.codeplex.com/releases/view/46280" target="_blank" title="coding guidelines">AvSol Coding Guidelines</a> the methods shouldn't contain more than 7 statements.</p>
<pre><strong><em>AV1500</em></strong><br /><em>Methods should not exceed 7 statements A method that requires more than 7 statements is doing too much, or has too many responsibilities. It also requires the human mind to analyze the exact statements to understand what the code is doing. Break it down in multiple small and focused methods with self-explaining names.</em></pre>
<h3>2. Don't nest conditional statement in deep levels in one method.</h3>
<p>For example it's hard for me to read some thing like:</p>
<pre><code>public void Method(){ <br />  if(condition 1){</code><code>       <br />    if(condition 2){<br /></code><code>       foreach(condition 3){</code><code>  <br />                if(condition 4){<br /></code><code>                        if(condition 5){<br /></code><code>                             ...</code><code> <br />                         }<br />                        else{<br /></code><code>  </code><code>                      }</code><code>      <br />                  }</code><code>      <br />        }</code><code> <br />      }<br /></code><code>  }<br /></code><code>}</code></pre>
<p>Break them into units. For example implement to like below looks cleaner:</p>
<pre><code>public void Method(){<br />  if(condition 1){<br />     if(condition 2){<br />         foreach(condition 3){<br />             Handle();<br />         }<br />     }<br />  }<br />}<br /><br /></code><code>public void Handle(){<br /></code><code> if(condition 4){<br /></code><code>     if(condition 5){<br /></code><code>             ...</code><code> <br /></code><code>     }<br /></code><code>     else{<br />          ...<br /></code><code></code><code>     }</code><code>      <br /></code><code> }<br /></code><code>}</code></pre>
<h3>3.Avoid Double Negative in Boolean conditions </h3>
<p>You can see how hard to understand as below example:</p>
<pre><code>var isNotSuccess = true;<br />...<br />if(!isNotSuccess)<br />{<br />   ... <br /></code><code>}</code></pre>
<p>Instead it's much easier to understand with below:</p>
<pre><code>var isSuccess = fase;<br />...<br />if(isSuccess)<br />{<br />  ...<br /></code><code>}</code></pre>
<h3> 4. Keep file name same as the type name.</h3>
<p>Consider the consistent seriously, and try to keep one <em>type</em> as a file and use the <em>namespace</em> according to the project relative directory path. it save others' effort to find and understand where is your code base. A typical mistake is forget to change the file name after modified the class name. Since it doesn't throw a compile error, this mistake will just be left behind.</p>
<p>In addition for partial type, the the source class should be the prefix, see below for example:</p>
<pre><code>Book.cs<br />//Partial Class. Good<br />Book.Extra.cs <br />//Partial Class. Bad<br />BookExtra.cs    </code></pre>
<h3><strong>5. Create a constant class to</strong> include<strong> the constant strings</strong></h3>
<p>Keep the common strings in a constant class not only make the code looks clean, it also helps to avoid misspell mistake. And it save effort to remember the variable names. A good practice is group them in nested classes. For example:</p>
<pre><code>public class MyConstantClass<br />{<br />   public const string SomeString= "SomeString"<br /></code><code>   public class Configuration<br />   {<br /></code><code>      public const string Name=""</code><code>       <br />   }<br />   public class Fields <br />   {<br />     public const  string Title="" <br />   }<br /></code><code>}</code></pre>
<p>Note that a const object is also a static, so it's not needed to be declared as static. The down site of this approach is it takes a bit more memory as it's creating all the values during compile time. </p>
<h3>6. Always add braces for a single statement.</h3>
<p>Well, It's been a debate on this. So it's only my opinion here, not suggest which one is better.</p>
<p>For example some prefer to put a statement like this:</p>
<pre><code>if(success) <br /></code><code>if(yes) return;</code></pre>
<p>It keeps it short and save the braces lines. However it also takes a bit of effort for add an extra statement later.</p>
<p>For me, I would prefer below:</p>
<pre><code>if(success){<br /></code><code>  if(yes){<br /></code><code>      return;</code><code> <br />  }<br /></code><code>}</code></pre>
<p> </p>
<h3>7. Create Methods for the long expressions in Linq.</h3>
<p>For example we have a code like below:</p>
<pre><code>public void SomeMethod<br />{<br />..<br />var query = CarLists.where(i =&gt; (i.Color == Option.Color&amp;&amp; i.Type == Option.Type &amp;&amp; i.Brand == Option.CarBrand) || Helper.IsRav4(i));<br />..<br />}</code></pre>
<p>It looks like it's a long expression, but this piece of code is not able to be reused. I would prefer to redactor it like below:</p>
<pre><code>public void SomeMethod<br />{<br />..<br />var query ==CarLists.Where(i =&gt; GetPromotedCar(i));<br />..<br />}<br /><br />private bool GetPromotedCar(Car i){<br />  if(Helper.IsRav4){<br />    Return true;  <br />  }<br />  if(</code><code>i.Color == Option.Color&amp;&amp; i.Type == Option.Type &amp;&amp; i.Brand == Option.CarBrand){<br />    Return true; <br />  }<br />  return false;<br /></code><span style="font-family: Verdana, Arial, Helvetica, sans-serif; background-color: #eeeeee;">}</span></pre>
<p>The benefit for using methods instead of long expressions is not only make it understandable, but also reusable, and unit testable.</p>
<h3>8. Avoid numerous Parameters in the methods.</h3>
<p>Say there is a method as below:</p>
<pre><code>public void CheckCar(string title, bool isFine, int speed, string Number, int seats){<br />  ...<br />} </code><code></code></pre>
<p>It will be hard to read and take more time to understand when calling the above method right? Compare to below:</p>
<pre><code>public void CheckCar(CarConditions conditions)<br />{<br /></code><code>  var title  = conditions.title;<br /></code><code>  var isFine = conditions.IsFine;<br /></code><code>  ...<br /></code><code>}</code></pre>
<p>There are a lot more of practices, there is also a good article to learn further:</p>
<p>https://msdn.microsoft.com/en-us/library/aa260844(v=vs.60).aspx</p>
<p>  </p>
