---
layout: post
title: 5 JavaScript basics that might drive c# Developers crazy
image: /img/blog/javascript.jpg
tags: [HTML5,CSS3,Javascript]
---
<p>Recently I developed a rich front app in JavaScript, while I am writing the code, I found that many things were not working as expected as I thought. There are some JavaScript basics just drive me a little bit crazy! Further inveterate, I find the five JavaScript rules that works a bit different you might find.</p>
<h4><strong>Basics 1: </strong>Fractions calculation is not precise.</h4>
<p><em>For example as below:</em></p>
<pre><code>var a=0.1;<br /></code><code>var b=0.2;<br /></code><code>if(a+b==0.3){</code><code> <br />  //False, it never goes here<br /></code><code>}</code></pre>
<p>Yeah, it doesn't work, go nuts!</p>
<p>According to <em>http://speakingjs.com/es5/ch11.html</em>, <em>"JavaScript, all numeric values are internally represented as floating point values. The 64-bit number is divided into three components: the fraction is 52 bits (bits 0 to 51), the exponent is 11 bits (bits 52 to 62), and the sign is a single bit (bit 63). "</em></p>
<p>To fix this problem, we need to round the results to truncate the fractions to a fixed number of decimals. For example as below: </p>
<pre><code>var a = 0.1;<br /></code><code>var b = 0.2;<br /></code><code>if((a+b).toFixed(1) == 0.3){</code><code> <br />  //Success, it will get to here<br /></code><code>}</code></pre>
<p>In a word, Fraction Calculation need to be taken extra care in JavaScript.  </p>
<h4><strong>Basics 2: </strong>Undefined Variable is not null or not give any error.</h4>
<p>If you do not use the var keyword to define the variable in the code, the variable is automatically created in a global scope.</p>
<p>see below example,</p>
<pre><code>function Book(){<br />   return {<br />       Price: basePrice + 5<br />   }<br /></code><code>};<br />basePrice = 5;<br /></code><code>var aBook = Book();<br />alert(aBook.Price)<br />//Output 10 instead of any error on console.</code></pre>
<p>I would say always use a var for every variable as a good practice. As it didn't  throw the error at console, it could make the app easily mess up the variables in local and global scopes</p>
<h4><strong>Basics 3:</strong> In JavaScript, array grow dynamically instead of fix length.</h4>
<p>say we have below array,</p>
<pre><code>var ids= [];<br />ids[0] = 1;<br />ids[1] = 2;<br />ids[8] = 9;<br />ids[4] = 5;</code><code><br /></code></pre>
<p>Do you know what's the length of the array? em.. it seams there is only 4 elements in it. However, the length is not 4. It's 9.</p>
<p>because the biggest index is 8, the array automatically grow itself until it reaches the last index. So the array will be look like below:</p>
<pre><code>var result = ids;<br /></code><code>//the result should be: [1, 2, undefined, undefined, 4, undefined, undefined, undefined, 9]</code><code></code></pre>
<p>Because of this basics, if you get a dynamic array, when looping through the array, we should always keep the best practice to check if the element is not undefined.</p>
<p><span class="highELE">Like below:</span></p>
<pre><code><span class="highELE">for</span><span> (i = </span><span class="highVAL">0</span><span>; i &lt; cars.length; i++) { </span></code><code><span>  <br />  if(cars[i]){<br /></span></code><code></code><code><span>    //do something...<br />  }<br /></span></code><code><span>}</span></code><code></code></pre>
<p>by the way any of the variable that is undefined, null, 0 or "", they are false in the conditional statement.</p>
<h4><strong>Basics 4: </strong>In JavaScript it use Function to define object.</h4>
<p>This is quite confuse c# developers who familiar with Class keyword, in JavaScript, it use the function to define an object. </p>
<pre><code>function Person(firstName, lastName)<br />{<br /></code><code>   this.fullName = firstName +" " + lastName;<br /></code><code>}<br />var student =new Person("Chris","P");<br />var result = student.fullName;<br />//resutls is "Chris P"</code><code> </code></pre>
<p>Note that <em>this</em> keyword here means the variable belongs to the object that owns the this function. The <em>new</em> keyword must be used to create an object from this class.</p>
<p>So Function <strong>≠</strong> Method,  it's also an object constructor.</p>
<h4><strong>Basics 5: </strong>In JavaScript different types of variable with same value are equal.</h4>
<p>see below example:</p>
<pre><code>if("10"==10)<br />{<br /></code><code>  //True, goes here<br /></code><code>}</code></pre>
<p>To perform a type and value absolute equality comparison, JavaScript use the === operators.</p>
<pre><code>if("10"===10)<br />{<br /></code><code>  //false, never goes here<br /></code><code>}</code></pre>
<p>however when come to calculation, they are treated differently, see below example</p>
<pre><code>var result = 10+"10";<br /></code><code>//result will be "1010" not 20<br /></code><code><strong><br />result = 10+Number("10")<br />//result as expected 20</strong></code></pre>
<p><strong> </strong>  </p>