---
layout: post
title: Tips to work with ASP.NET MVC view
image: /img/blog/view.jpg
tags: [ASP.NET MVC]
---
<p>The View is part of the Model-View-Controller design pattern, it determines how to present the page in a browser. The view should be easily understandably by both back-end developers and front-end developers to work on.</p>
<p>So there are some of the key points I should would like to share what to consider when working with the view:</p>
<p><strong>Should use Strongly typed views. </strong>R<span>endering specific types of model objects, instead of using the general ViewData/ViewBag structure. So it's convenient for just use the IntelliSense property of the model class.</span></p>
<p><span>For example, a</span> bad one is like below:</p>
<pre><span>@{<br />  var firstName = ViewBag.FirstName;<br />}<br />&lt;div&gt;<br /> @firstName<br />&lt;/div&gt;</span></pre>
<p><span>A good one should be:</span></p>
<pre>@inherits MyNameSpace.Person<br /><br />&lt;div&gt; <br /> @Model.FirstName<br />&lt;div&gt;</pre>
<p><strong>Should use View Model not the Data Model.</strong> Data Model is usually defined in the Data/Domain layer, View Model sit usually in the presentation layer.<strong> </strong>Use the Data Model in the View to pass in a few of the property is a bad practice, and it could be hard to maintain . The proper way is use the view model that is designed specifically for certain type of view, and it should only map the necessary property from the Data Model.</p>
<p><span><strong>Should consider use Partial View instead of a long code block in one view.</strong> For a block code of a component or the pieces is repeated in many other views, you should break some components into partial views. so they are re-usable and easier to maintain.</span></p>
<p><strong>Should create a layout page if the views share similar structure. </strong>Don't just copy and past to create a new View, this will make the code duplicated, which makes the view files hard to maintain.</p>
<p><strong>Never put business logic code in the View. </strong>The reason we embrace the MVC here is because it is very naturally separates the presentation and business layers. Ideally, the code put in the view should only serve the purpose to display the information. Writing business logic code in the view makes it hard to read and understand, especially for the web designer who isn't familiar with the back-end code.</p>
<h3>In conclusion:</h3>
<p>When designing a view, we should always follows the MVC framework separation of concept (SoC) rules and make sure the view is clean, reusable and maintainable.</p>
<p>If you have any other suggestions, you are welcomed to comment.</p>