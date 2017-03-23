---
layout: post
title: How to prevent double click on the form?
image: /img/blog/form.jpg
tags: [ASP.NET MVC,Javascript]
---
<p>We should never count on users that they should just click on the button once, if there is a chance goes wrong, it will happen. Double click on the submit button can result into some issues, for example, duplicated records inserted into data, multiple process running in parallel unintended.</p>
<p>The simplest solution is disable the submit button after a click, code as below:</p>
<pre class="default prettyprint prettyprinted">&lt;form&gt;<br /> &lt;input type="text" /&gt;<br /> &lt;input type="submit" value="submit" onclick="this.disabled=true;"&gt;<br /> &lt;form/&gt;
</pre>
<p>However, while there is a validation failure, then we need to enable the button again, in this case, we can add JavaScript listener to watch the text field and enable the submit attribute.</p>
<pre>$("input[type=text]").on('keyup',function(){
  $("input[type=submit]:disabled").prop('disabled', false);
});

</pre>
<p>try test it out in <a href="https://jsfiddle.net/wyyv3byc/7/">https://jsfiddle.net/wyyv3byc/7/</a></p>
<p>In some case case, you probably need to make it friendly display the waiting message after click and pending for the server response.</p>
<p> </p>